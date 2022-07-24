redirect uri 로 코드 값을 받게 된다.

받은 코드값을

```java
//controller
@GetMapping(value="/oauth/kakao")
public ResponseEntity login(@RequestParam("code") String code) {
  String access_Token = oAuthService.getKakaoAccesToken(code);

    return ResponseEntity.ok().body(jwtToken);
}
```

```java
//service
public String getKakaoAccesToken(String code) {
  String access_Token = "";
  String refresh_Token = "";
  String reqURL = "https://kauth.kakao.com/oauth/token";

  try {
    URL url = new URL(reqURL);
    HttpURLConnection conn = (HttpURLConnection) url.openConnection();

    conn.setRequestMethod("POST");
    conn.setDoOutput(true);

    //post parameter
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(conn.getOutputStream()));
    StringBuilder sb = new StringBuilder();
    sb.append("grant_type=authorization_code");
    sb.append("&client_id=12e312jb12ab112j8812f64322712f5b01"); // REST_API_KEY
    sb.append("&redirect_uri=http://localhost:3000/oauth/kakao"); // 인가코드 받은 redirect_uri
    sb.append("&code=" + code);
    bw.write(sb.toString());
    bw.flush();

    //결과 코드가 200이라면 성공
    int responseCode = conn.getResponseCode();
    System.out.println("responseCode = " + responseCode);
    System.out.println("service-1");


    //요청을 통해 얻은 JSON타입의 Response 메세지 읽어오기
    BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
    String line = "";
    String result = "";

    while ((line = br.readLine()) != null) {
      result += line;
    }

    //Gson 라이브러리에 포함된 클래스로 JSON파싱 객체 생성
    JsonParser parser = new JsonParser();
    JsonElement element = parser.parse(result);

    access_Token = element.getAsJsonObject().get("access_token").getAsString();
    refresh_Token = element.getAsJsonObject().get("refresh_token").getAsString();

    System.out.println("access_token : " + access_Token);
    System.out.println("refresh_token : " + refresh_Token);

    br.close();
    bw.close();

  } catch (IOException e) {
    throw new RuntimeException(e);
  }
  return access_Token;
}
```

HttpURLConnection 를 사용해 api호출한다.

호출 값이 200이면 성공하게 된다.

성공적으로 받은 값을 gson라이브러리를 이용해 json파싱 객체 생성한다.



kakao에서 제공한 access_token, refresh_token은 kakao 회원의 개인정보를 조회할 수 있기 때문에 조심해서 백엔드에서만 핸들링해야 한다. client에 보내는 토큰은 자체 서버에서 발급해서 전송해야 안전하다.