# Kotlin extension functions for MockServer

This library adds `MockServerClient.given` extension function
which is an alias for `MockServerClient.when`, but since `when`
is a keyword in Kotlin it has to be wrapped into quotes.

In addition the library implements it's own `request` function,
which lets you build requests in a more compact way:

```kotlin
mockServerClient
    .given(
        request(
            method = "GET",
            path = "/cars",
            queryParameters = listOf("min_year" to "2018"),
            headers = listOf("Accept-Encoding" to "gzip")
        )
    )
    .respond(response()
        .withHeader("Content-Type", "application/json")
        .withBody("""
            [{
              "id": "2afea46e-5c40-4c62-a0cb-2e594ecc6777",
              "car_make": "Volkswagen",
              "car_model": "Golf",
              "color": "Turquoise",
              "image": "http://dummyimage.com/213x218.bmp/5fa2dd/ffffff"
            }, {
              "id": "9f88dbe5-0bcb-42f8-bb22-41d327d22324",
              "car_make": "Pontiac",
              "car_model": "Fiero",
              "color": "Aquamarine",
              "image": "http://dummyimage.com/164x167.png/cc0000/ffffff"
            }, {
              "id": "3d259458-8e59-457d-a0c7-e98020e14287",
              "car_make": "Oldsmobile",
              "car_model": "Ciera",
              "color": "Aquamarine",
              "image": "http://dummyimage.com/150x145.bmp/5fa2dd/ffffff"
            }]""".trimIndent()
        )
    )
```
