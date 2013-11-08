### [&laquo; Home](README.md)

[Bukalapak Messages API](#bukalapak-negotiations-api)
- [Get Inbox](#get-inbox)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Get Conversation](#get-conversation)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Get Message](#get-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Create Message](#create-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [POST request data](#post-request-data)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Delete Conversation](#delete-conversation)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)
- [Delete Message](#delete-message)
	- [Resource URL](#resource-url)
	- [Parameters](#parameters)
	- [Example Request](#example-request)
	- [Example Response](#example-response)

## Bukalapak Messages API

### Get Inbox
Get current user's inbox

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages.json]().

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages.json?page=1
````

##### Example Response
````json
{
	"status":"OK",
	"unread":0,
	"inbox":[{"id":"518d0d42318b276640000009","updated_at":"2013-07-04T11:47:35+07:00","partner_id":"6","partner_name":"Administrator","user_id":"15","user_name":"Me Ow"},{"id":"515417c4318b273063000014","updated_at":"2013-04-18T23:01:18+07:00","partner_id":"46688","partner_name":"Cust.Service BukaLapak ","user_id":"15","user_name":"Me Ow"}]
}
````

### Get Conversation
Get current user's selected conversation

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/:id.json]().

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages/516d3299425762188f000011.json
````

##### Example Response
````json
{
	"status":"OK",
	"instant_messages":[{"_id":"516e2565177961034c000002","attachment_id":0,"body":"tesssss","body_bb":"tesssss","category":0,"created_at":"2013-04-17T11:30:29+07:00","inbox_id":"516d3299425762188f000011","product_id":null,"read":true,"receiver_id":"110675","receiver_name":"Phillip Leonardo","removed":false,"sender_id":"110677","sender_name":"Testa B","updated_at":"2013-04-17T11:30:29+07:00"}],
	"message":null
}
````

### Get Message
Get current user's selected message

+ Use `GET` http method.

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/im/:id.json]().

##### Parameters
None

##### Example Request
````sh
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v1/messages/im/516e2565177961034c000002.json
````

##### Example Response
````json
{
	"status":"OK",
	"instant_message":{"_id":"516e2565177961034c000002","attachment_id":0,"body":"tesssss","body_bb":"tesssss","category":0,"created_at":"2013-04-17T11:30:29+07:00","inbox_id":"516d3299425762188f000011","product_id":null,"read":true,"receiver_id":"110675","receiver_name":"Phillip Leonardo","removed":false,"sender_id":"110677","sender_name":"Testa B","updated_at":"2013-04-17T11:30:29+07:00"},
	"message":null
}
````

### Create Message
Create a new message

+ Use `POST` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages.json]().

##### Parameters
None

##### POST request data
+ `instant_message` *(required)*. New message to be sent, which contains:
	+ `receiver_id` *(required)*. Message receiver's user ID
	+ `category` *(required)*. Message category: '0' => normal message, '1' => question, '2' => suggestion, '3' => feature, '4' => transaction, note that for category > 0 must be addressed to admin
	+ `body_bb` *(required)*. Message's content

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH -d '{ "instant_message":{"receiver_id":"110675", "category":"0", "body_bb":"tesssss"} }' https://api.bukalapak.com/v1/messages.json -H "Content-Type: application/json" -X POST
```

##### Example Response
Failed example
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Gagal mengirim pesan: harap menggunakan format yang seharusnya"
}
```
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Gagal mengirim pesan"
}
```
```json
{
	"status":"ERROR",
	"id":null,
	"message": "Pengiriman pesan untuk kategori ini hanya dapat ditujukan kepada admin"
}
```
Successfull example
```json
{
	"status":"OK",
	"id":"516d303c425762188f000007",
	"message": null
}
```

### Delete Conversation
Delete existing conversation

+ Use `DELETE` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being destroy.

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v1/messages/516d3299425762188f000011.json -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"516d3299425762188f000011",
	"message": "Conversation berhasil dihapus"
}
```

### Delete Message
Delete existing message

+ Use `DELETE` http method.
+ Requires authentication

##### Resource URL
+ [https://api.bukalapak.com/v1/messages/im/:id.json]().

##### Parameters
+ `id` *(required)*. Identifier for product being destroy.

##### Example Request
```sh
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v1/messages/516d3299425762188f000015.json -H "Content-Type: application/json" -X DELETE
```

##### Example Response
Successfull example
```json
{
	"status":"OK",
	"id":"516d3299425762188f000015",
	"message": "Pesan berhasil dihapus"
}
```
