# Steps for contributing

If not already on your machine install [symfony](https://symfony.com/download).

Make sure you have the necessary php extensions available in your PHP runtime and other [requirements](https://symfony.com/doc/current/setup.html#technical-requirements) met to run symfony.

## Migrate Database
After creating a user and database with the relevant permissions you can run:
```
$ bin/console doctrine:schema:update --force
```

## Add Admin user
```
$ bin/console unite:user:create
Please select a UniteUser type:
  [Admin    ] Admin
  [OtherUser] OtherUser
 > Admin
Please select a username:admin
Please select a password:
```

## Generate private/public keys

It is nessecary to generate a private & public key pair so JWT auth can function.
If you get this error you probably missed the step.
```
An error occurred while trying to encode the JWT token
```

### Create the config/jwt directory
```
$ mkdir config/jwt
```

### Generate the private key
Make sure to enter the password configured in .env variable "JWT_PASSPHRASE".
```
$ openssl genrsa -out config/jwt/private.pem -aes256 512
Generating RSA private key, 512 bit long modulus (2 primes)
............+++++++++++++++++++++++++++
....+++++++++++++++++++++++++++
e is 65537 (0x010001)
Enter pass phrase for config/jwt/private.pem:
Verifying - Enter pass phrase for config/jwt/private.pem:
```

### Generate the public key
Use the same password as in the previous step.
```
$ openssl rsa -in config/jwt/private.pem -outform PEM -pubout -out config/jwt/public.pem
Enter pass phrase for config/jwt/private.pem:
writing RSA key
```


## Start Developing
### Symfony
```
$ symfony serve
```
### Vue
Compile the Vue code to the app.js bundle using [encore](https://symfony.com/doc/current/frontend/encore/vuejs.html) (supports hot reloading)

```
$ yarn encore dev-server --hot
```