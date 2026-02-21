# HTBash

Command-line tool written in Bash to list and query Hack The Box machines via the HTB API.

## Requirements

- curl
- jq
- Hack The Box API token

## Installation

```bash
git clone https://github.com/n0m3l4c000nt35/htbash.git
cd htbash
chmod +x htbash
```

Store your API token:

```bash
mkdir -p $HOME/.config/htb
echo "APP_TOKEN" > $HOME/.config/htb/htbash.conf
```

Install system-wide:

```bash
sudo ln -s $(pwd)/htbash /usr/bin/htbash
```

## Usage

```
htbash [OPTIONS]
```

### Options

| Flag | Description |
|------|-------------|
| `-u` | Sync machine list from the HTB API |
| `-l` | List all available machines |
| `-i <machine>` | Show detailed info for a machine |

### Filters (use with `-l`)

| Flag | Values | Description |
|------|--------|-------------|
| `--os` | `linux`, `windows`, `android` | Filter by OS |
| `--difficulty` | `easy`, `medium`, `hard`, `insane` | Filter by difficulty |
| `--free` | — | Show only free machines |
| `--owned` | `y`, `n` | Filter by owned status |

## Examples

```bash
# Sync machine list
htbash -u

# List all machines
htbash -l

# Show machine info
htbash -i Lame

# Easy Linux machines
htbash -l --os linux --difficulty easy

# Free machines only
htbash -l --free

# Owned machines
htbash -l --owned y

# Hard Windows machines not yet owned
htbash -l --os windows --difficulty hard --owned n
```

## Configuration

The API token must be stored in `$HOME/.config/htb/htbash.conf`. The machine cache is saved to `$HOME/.config/htb/machines/machines.json` after running `-u`.

## Troubleshooting

**Machine not found** — run `htbash -u` to sync the machine list and verify the name is correct.

**API connection error** — check that your token in `~/.config/htb/htbash.conf` is valid.
