# Невеликий web додаток для демонстрації роботи RSA

Після запуску додатку, вам будуть доступні 4 endpoints для роботи з RSA.
Всі запроси повинні містити заголовки "Username" та "Password". Данні зберігаються в файлі credentials.txt 
у вигляді username:password, які загешованні за допомогою sha256.

В ньому вже зберігається користувач із логіном `user` та паролем `password`.

#### Отримання публічного ключа користувача
````
curl --location --request GET 'http://localhost:8080/key' \
   --header 'Username: user' \
   --header 'Password: password'
````

#### Генерація нових ключей для користувача
````
curl --location --request POST 'http://localhost:8080/generateKeys' \
   --header 'Username: user' \
   --header 'Password: password'
````

#### Запит на шифрування 
```` 
curl --location --request POST 'http://localhost:8080/encrypt' \
   --header 'Content-Type: application/json' \
   --data-raw '{
       "publicKey": {
           "n": 130566606325752874537071781694616593426807309016669762558872719761161456195238524285805518161214348534442517411531973154091896204636200245419245171918829988478975065467018957801928631207351587387742751883042612409057134219977617887501253806328216259789502485606642338770379102059874769898718592029566157162381,
           "e": 65537
       },
       "message": "123456789_123456789_123456789_123456789_123456789_123456789_123456789_123456789_123456789_123456789_123456789_123456789_12345678"
   }'
````

#### Запит на розшифрування
````
curl --location --request POST 'http://localhost:8080/decrypt' \
    --header 'Username: user' \
    --header 'Password: password' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "encryptedMessage": "26744891781952124451598620672900234925349986667183780081991474993746542755269528447278779807140243663952550450845002162556271619188500113100220472025373097841545832846631791716609876961938644864450632083248405260303837135499313069604556789940212367999418155286607835978825079038386571078882931631604927776565"
    }'
````