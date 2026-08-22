# pushinbr/pam-testing

Fast in-memory tests for applications built with `pushinbr/pam-http`.

## Start here

PAM Testing is a Composer package for applications running on the PAM Runtime;
it is not a standalone test runtime. Install PAM first, open your application
directory, and add the development package through PAM's Composer toolchain:

## Start here

PAM Testing is a Composer package for applications running on the PAM Runtime;
it is not a standalone test runtime. Install PAM first, open your application
directory, and add the development package through PAM's Composer toolchain:

```bash
curl --proto '=https' --proto-redir '=https' --tlsv1.2 \
    --connect-timeout 15 --max-time 60 --max-filesize 1048576 -fsSL \
    https://github.com/push-in/pam/releases/latest/download/install.sh | sh

pam doctor
cd my-app
pam composer require --dev pushinbr/pam-testing
```

```php
$client = new Pam\Testing\TestClient($app);
$client->get('/users/42')
    ->assertSuccessful()
    ->assertJsonPath('id', '42');
```

The client invokes the application pipeline without opening a network port. Use
Pam's Rust integration suite for transport, timeout and protocol behavior.

## License

Free and open-source under the [Apache License 2.0](LICENSE). You may use,
modify, and distribute this package for any purpose, including commercially.


## Recommended PAM workflow

Add the testing client to an existing project with `pam composer require --dev pushinbr/pam-testing`. Run the test suite through PAM with `pam composer test` or the script defined by your project.

Run `pam doctor` after dependency changes and before creating a release. The project remains a normal Composer project with a standard manifest, lockfile, PSR-4 autoloading, and `vendor/autoload.php`.

## API guide

| Surface | Use it for |
| --- | --- |
| `TestClient` | Issue in-memory `request()`, `get()`, and `postJson()` calls. |
| `TestResponse::assertStatus()` | Assert an exact status code. |
| `assertSuccessful()` | Assert a 2xx response. |
| `assertHeader()` | Assert header presence or value. |
| `assertJson()` | Assert decoded JSON contains expected values. |
| `assertJsonPath()` | Assert a dot-path inside decoded JSON. |

The client executes the application pipeline without opening a socket, making route and middleware tests fast and deterministic. It does not replace PAM's Rust integration suite for TLS, HTTP framing, timeout, streaming, cancellation, or backpressure behavior.

## Production checklist

- Keep request data and mutable state scoped to the current request.
- Test success, validation failure, exception, cancellation, and timeout paths.
- Configure explicit limits and avoid unbounded payloads, queues, or retained collections.
- Run `pam doctor`, `pam test`, and the relevant integration suite before release.
- Validate real dependencies and workload behavior; compatibility is not inferred from package installation alone.

## Troubleshooting

- **Class not found:** run `pam composer install`, verify PSR-4 configuration, and rerun `pam doctor`.
- **Behavior differs over the network:** reproduce with PAM's transport integration tests; in-memory execution does not model the socket boundary.
- **A dependency blocks a worker:** use PAM-native I/O, a compatible event loop, a process pool, or additional isolated workers.

## Documentation and support

- [PAM introduction](https://push-in.github.io/pam-docs/introduction/)
- [Package ecosystem](https://push-in.github.io/pam-docs/packages/overview/)
- [Runtime compatibility](https://push-in.github.io/pam-docs/runtime/compatibility/)
- [Report an issue](https://github.com/push-in/pam-testing/issues)

Report security vulnerabilities through GitHub private vulnerability reporting or the PAM security policy, not a public issue.
