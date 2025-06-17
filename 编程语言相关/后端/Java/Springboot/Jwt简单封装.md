## 引入

gradle:
```gradle
implementation 'com.auth0:java-jwt:4.4.0'
```

`JwtUtil`
```java
public class JwtUtil {

    private static final String KEY = "hoso";
    private static final Integer EXPIRATION_DATE= 1000 * 60 * 60 * 12;
	
	//接收业务数据,生成token并返回
    public static String genToken(Map<String, Object> claims) {
        return JWT.create()
                .withClaim("claims", claims)
                .withExpiresAt(new Date(System.currentTimeMillis() + EXPIRATION_DATE))
                .sign(Algorithm.HMAC256(KEY));
    }

	//接收token,验证token,并返回业务数据
    public static Map<String, Object> parseToken(String token) {
        return JWT.require(Algorithm.HMAC256(KEY))
                .build()
                .verify(token)
                .getClaim("claims")
                .asMap();
    }

}
```