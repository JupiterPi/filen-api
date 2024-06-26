# Guides

## Login

- fetch salt from `/v3/auth/info`, use as string or byte array (do not try to decode string)
- compute derived password as sha512-PBKDF2 of raw password with above salt and 200000 iterations
- compute transmission password as sha512 hash of second half of derived password
- pass into `/v3/login`


## List directory

- fetch uuid of base directory from `/v3/user/baseFolder`