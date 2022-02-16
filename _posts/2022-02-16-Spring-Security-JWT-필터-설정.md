config.SecurityConfig 생성



``` java
import com.example.jwt.config.jwt.JwtAuthenticationFilter;
import com.example.jwt.config.jwt.JwtAutorizationFilter;
import com.example.jwt.repository.UserRepository;

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.web.filter.CorsFilter;

import lombok.RequiredArgsConstructor;

@Configuration //IOC
@EnableWebSecurity //시큐리티 확성화
@RequiredArgsConstructor //DI
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    
  	//DI
    private final CorsFilter corsFilter;
    private final UserRepository userRepository;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable();
        http.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) //세션 생선 X
        .and()
        .addFilter(corsFilter) //cors 모두 허용, 시큐리티 필터에 등록 인증 (0)
        .formLogin().disable() //spring formLogin 사용 안함
        .httpBasic().disable() //
        .addFilter(new JwtAuthenticationFilter(authenticationManager())) // AuthenticationManeger
        .addFilter(new JwtAutorizationFilter(authenticationManager(),userRepository)) // AuthenticationManeger
        .authorizeRequests()
        .antMatchers("/api/v1/user/**")
        .access("hasRole('ROLE_USER') or hasRole('ROLE_MANAGER') or hasRole('ROLE_ADMIN')")
        .antMatchers("/api/v1/manager/**")
        .access("hasRole('ROLE_MANAGER') or hasRole('ROLE_ADMIN')")
        .antMatchers("/api/v1/admin/**")
        .access("hasRole('ROLE_ADMIN')")
        .anyRequest().permitAll();
    }

}
```



config.CorsConfig 생성 (CorsError 방지)

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;
import org.springframework.web.filter.CorsFilter;

@Configuration
public class CorsConfig {
    
    @Bean
    public CorsFilter corsFilter() {
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        CorsConfiguration config = new CorsConfiguration();
        config.setAllowCredentials(true); // json 을 응답할때 js에서 처리할 수 있게 할지 설정
        config.addAllowedOrigin("*"); // 모든 ip 응답 허용
        config.addAllowedHeader("*"); // 모든 header 응답 허용
        config.addAllowedMethod("*"); // 모든 method 응답 허용
        source.registerCorsConfiguration("/api/**", config);
        return new CorsFilter(source);
    }
}

```

