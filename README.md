# Laravel Boilerplate 

Create Laravel Project with Sail
```
curl -s "https://laravel.build/plate" | bash
cd plate && ./vendor/bin/sail up -d
```

sail helper function
```
function sail() {
  ./vendor/bin/sail $@
}
```

Goto: http://localhost/

# Authentication

## -either- Breeze (simpler)
```
sail composer require laravel/breeze --dev
sail php artisan breeze:install
sail npm install
sail npm run dev
sail php artisan migrate
```

## -or- Jetstream

todo


# LDAP (Ldaprecord)

```
sail composer require directorytree/ldaprecord-laravel
sail php artisan vendor:publish --provider="LdapRecord\Laravel\LdapServiceProvider"

# configure config/ldap.php OR put in 
LDAP_LOGGING=true
LDAP_CONNECTION=default
LDAP_HOST=
LDAP_USERNAME="cn=user,dc=local,dc=com"
LDAP_PASSWORD=
LDAP_PORT=389
LDAP_BASE_DN="dc=local,dc=com"
LDAP_SSL=false
LDAP_TLS=false

# test connection:
sail php artisan ldap:test
```


#  AdminLTE Installation (notes from the original docs)

Full reference: https://github.com/jeroennoten/Laravel-AdminLTE/wiki/Installation

```
sail composer require jeroennoten/laravel-adminlte
sail php artisan adminlte:install
sail php artisan adminlte:install --only=main_views
```

Copy example basic page from examples to `resources/views`
```
cp -fv ../examples/home.blade.php resources/views/home.blade.php
```


# Livewire

while installing, listen to: https://open.spotify.com/track/6FWoYwZa13llS7nj0SG65F  
this is mandatory! otherwise it won't work! trust me.

https://laravel-livewire.com/docs/2.x/quickstart

```
sail composer require livewire/livewire
sail php artisan vendor:publish --tag=livewire:config
```






## HTTPS / Proxy

To use a https reverse proxy, you need to force https.
Add to `app/Providers/AppServiceProvider.php`:
```bash
    public function boot()
    {
        \Illuminate\Support\Facades\URL::forceScheme('https');
    }
```
