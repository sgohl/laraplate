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
sail artisan breeze:install
sail npm install
sail npm run dev
sail artisan migrate
```

## -or- Jetstream

todo


# LDAP (Ldaprecord)
https://ldaprecord.com/docs/laravel/v2/
```
sail composer require directorytree/ldaprecord-laravel
sail artisan vendor:publish --provider="LdapRecord\Laravel\LdapServiceProvider"

# .env
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
sail art ldap:test
```

#  AdminLTE

Full reference: https://github.com/jeroennoten/Laravel-AdminLTE/wiki/Installation

```
sail composer require jeroennoten/laravel-adminlte
sail artisan adminlte:install
#? sail artisan adminlte:install --only=main_views
```

Replace the breeze-distributed default dashboard blade template:
```
# resources/views/dashboard.blade.php

@extends('adminlte::page')

@section('title', 'Dashboard')

@section('content_header')
    <h1>Dashboard</h1>
@stop

@section('content')
    <p>Welcome to this beautiful admin panel.</p>
@stop

@section('css')
    <link rel="stylesheet" href="/css/admin_custom.css">
@stop

@section('js')
    <script> console.log('Hi!'); </script>
@stop
```


# Livewire

https://laravel-livewire.com/docs/2.x/quickstart
```
sail composer require livewire/livewire
sail artisan vendor:publish --tag=livewire:config
```

# Laravel Echo / Websockets

old:
https://beyondco.de/docs/laravel-websockets/getting-started/installation

```
# as for now, 2021-12-17, installation fails (deps); workaround:
sail composer require guzzlehttp/psr7:^1.5

sail composer require beyondcode/laravel-websockets
sail artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="migrations"
sail artisan migrate
sail artisan vendor:publish --provider="BeyondCode\LaravelWebSockets\WebSocketsServiceProvider" --tag="config"

# port 6001
sail artisan websockets:serve
```

## Socket.io
https://github.com/tlaverdure/laravel-echo-server
```
sail npm install laravel-echo-server
sail bash
./node_modules/laravel-echo-server/bin/server.js init
```
modify `laravel-echo-server.json`
```
	"database": "redis",
	"databaseConfig": {
		"redis" : {
			"port": "6379",
			"host": "redis"
		},

```
start
```
./node_modules/laravel-echo-server/bin/server.js start
```

# Routes

example route for `routes/web.php`
```
Route::get('/example', function () {
    return view('example');
});
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
