Cross-Origin Resource Sharing (CORS) is essential in web applications to enable or restrict resources on a web server to be requested from another domain outside the domain from which the resource originated. In a Spring Boot application, you often need to configure CORS to allow web applications hosted on different domains to communicate with your server.

### Understanding CORS
#### Same-Origin Policy

Web browsers enforce the Same-Origin Policy (SOP), which restricts how resources on a web page can be requested from another domain, subdomain, or protocol. For example, a script running on `https://example.com` cannot make an AJAX request to `https://anotherdomain.com` due to the SOP.

#### Cross-Origin Resource Sharing (CORS)

CORS relaxes the restrictions imposed by the SOP by allowing servers to specify who can access their resources and how those resources can be accessed. This is done using specific HTTP headers.
If the server allows the cross-origin request, it responds with appropriate CORS headers. Otherwise, the browser blocks the request.

### Key CORS Headers

1. **`Access-Control-Allow-Origin`**:
    
    - Specifies which origins are permitted to access the resource.
    - Example: `Access-Control-Allow-Origin: https://example.com` or `Access-Control-Allow-Origin: *` (to allow any origin).
2. **`Access-Control-Allow-Methods`**:
    
    - Specifies the HTTP methods that are allowed when accessing the resource.
    - Example: `Access-Control-Allow-Methods: GET, POST, PUT, DELETE`.
3. **`Access-Control-Allow-Headers`**:
    
    - Specifies the headers that can be used in the actual request.
    - Example: `Access-Control-Allow-Headers: Content-Type, Authorization`.
4. **`Access-Control-Allow-Credentials`**:
    
    - Indicates whether the request can include user credentials (cookies, HTTP authentication).
    - Example: `Access-Control-Allow-Credentials: true`.
5. **`Access-Control-Expose-Headers`**:
    
    - Specifies which headers are safe to expose to the client.
    - Example: `Access-Control-Expose-Headers: X-Custom-Header`.
6. **`Access-Control-Max-Age`**:
    
    - Indicates how long the results of a preflight request can be cached.
    - Example: `Access-Control-Max-Age: 86400` (24 hours).

### Example
Here’s an example of how CORS headers might look in an HTTP response from the server:
```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 3600
Content-Type: application/json
```

### Example of Preflight Request and Response
#### Preflight Request (HTTP OPTIONS)
```
OPTIONS /resource HTTP/1.1
Host: api.example.com
Origin: https://example.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Content-Type
```

#### Preflight Response (HTTP 200 OK)
```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: POST
Access-Control-Allow-Headers: Content-Type
Access-Control-Max-Age: 86400
```

### Enabling CORS in a Spring Boot Application
To enable CORS in a Spring Boot application, you can use the `@CrossOrigin` annotation or define a `CorsConfigurationSource` bean.

#### Using `@CrossOrigin`
```
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @CrossOrigin(origins = "https://example.com")
    @GetMapping("/resource")
    public String getResource() {
        return "Hello, CORS!";
    }
}
```

#### Using `CorsConfigurationSource`
```
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
        config.setAllowCredentials(true);
        config.addAllowedOrigin("https://example.com");
        config.addAllowedHeader("*");
        config.addAllowedMethod("*");
        source.registerCorsConfiguration("/**", config);
        return new CorsFilter(source);
    }
}
```

