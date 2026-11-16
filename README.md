# Example DNS plugin for Databasify

A working [Databasify](https://github.com/databasifylabs/databasify) plugin and a template to start your own. It adds **Example DNS**, a fake DNS provider that keeps records in a JSON file, so you can try the whole plugin flow offline.

## Try it

1. In Databasify, open **Plugins**, click **Install plugin** and enter `databasifylabs/plugin-example-dns`, or upload a zip of this repository.
2. Open **DNS → Add**, pick **Example DNS** and fill in any account name and token, for example `demo` and `secret`.
3. The zones `example-dns.test` and `demo.test` appear. Point a database at one of them.

Records are written to `storage/app/example-dns/<sha1 of account:token>.json`. Each record the plugin creates carries the `DnsRecord::MARKER` comment, so Databasify knows it manages it. Uninstalling the plugin deletes that folder.

## Layout

```
plugin.json                                 key, name, version, author, class, autoload
src/ExampleDnsPlugin.php                    the plugin, a Laravel service provider
src/ExampleDns.php                          the DNS driver
src/StoredRecord.php                        one record as stored in the JSON file
public/icon.svg                             plugin icon, shown on the Plugins page
public/icons/dns-providers/example-dns.svg  DNS provider icon
```

## Start your own plugin from this template

1. Set your own `key` (`vendor/name`), `name` and `author` in `plugin.json`. The key identifies the plugin, so two vendors can use the same name.
2. Rename the namespace in `autoload` and in every file under `src/`.
3. Rename the plugin class and update `class`.
4. Change the provider id returned by `id()` and the label passed to `->label()`.
5. Rename the provider icon to `public/icons/<kind>-providers/<your id>.svg` and replace `public/icon.svg`.
6. Set `requires` to the Databasify versions you support.
7. Replace the fake driver with calls to your provider's API.

The full guide, with every builder method and driver contract, is at [docs.databasify.io](https://docs.databasify.io/plugins/writing-plugins/).

## Security

A plugin is PHP code that runs with Databasify's full access. Install only plugins you trust.
