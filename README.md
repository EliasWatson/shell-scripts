# Shell Scripts
My personal collection of useful shell scripts.

## Requirements
| Name                                                     | Description                                     |
| ---                                                      | ---                                             |
| [slap](https://github.com/agnipau/slap)                  | Argument parsing                                |
| [eva](https://github.com/NerdyPepper/eva)                | Calculator. Replacement for `bc`                |
| [jq](https://github.com/stedolan/jq)                     | JSON parsing                                    |
| [uuid-v4-cli](https://github.com/ken-matsui/uuid-v4-cli) | UUID generation                                 |
| [random-cli](https://github.com/AmrSaber/random-cli)     | Random number generation _(Looking to replace)_ |

## Scripts
### `json_fmt`
Format a JSON file with jq.

```console
$ cat example.json
{ "key": 42, "numbers": [1, 2, 3] }
$ json_fmt example.json
$ cat example.json
{
  "key": 42,
  "numbers": [
    1,
    2,
    3
  ]
}
```

### `json_merge`
Merge a JSON dictionary from STDIN with a JSON file.
The file does not have to exist.

A custom jq filter for merging can be passed with `--merge-filter`/`-m`.
By default, it is `.[0] * .[1]`.

```console
$ cat example.json
{
  "item_1": {
    "name": "First Item"
  },
  "item_2": {
    "name": "Second Item"
  }
}
$ echo '{ "item_3": { "name": "Third Item" } }' | json_merge example.json
$ cat example.json
{
  "item_1": {
    "name": "First Item"
  },
  "item_2": {
    "name": "Second Item"
  },
  "item_3": {
    "name": "Third Item"
  }
}
```

### `pad_num`
Pad an integer number with zeros to a specific length.

The number can be passed as an argument with `pad_num <digits> <num>`.
Or it can be passed through STDIN with `... | pad_num <digits>`.

### `timestamp`
Get the current Unix timestamp.

- In seconds: `timestamp` or `timestamp s`
- In milliseconds: `timestamp ms`
- In nanoseconds: `timestamp ns`

### `sleep_rand`
Sleep for a random amount of time.
By default, 0.5 to 1.5 seconds.

The range can be specified with the `--lower-bound`/`-l` and `--upper-bound`/`-u` arguments.
The upper bound can be a number (eg. `5`) or an offset from the lower bound (eg. `+2.3`).

### `temp_store`
Create temporary files.
A unique path is automatically generated, so collisions are avoided.

A session can be generated with `temp_store session <name>`, where `name` is the name of your program/script.
A UUID will be returned through STDOUT.

File paths can be generated with `temp_store file <uuid> <name>`, where `uuid` is the UUID of the session and `name` is the name of the file.

