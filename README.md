# colitop

A minimal htop-style terminal monitor for [Colima](https://github.com/abiosoft/colima).

It shows, refreshed live:

- **VM meters**: CPU, memory and the Docker data disk inside the Colima VM
- **Running containers**: CPU %, memory, memory %, PIDs and network I/O
- **Volumes**: size, whether a container uses it, and its Compose / Supabase project
- **Totals**: image size, reclaimable space, volumes and build cache

```
 colitop  profile: personal  context: colima-personal                  23:21:19

 CPU  [||                                      ]   6.1%  2 cpus
 MEM  [||||||||||||                            ]  30.5%  1.2G / 3.8G
 DISK [|||||||||||||                           ]  31.3%  6.1G / 19.5G

 CONTAINERS (8)  sorted by cpu
 NAME                                        CPU%        MEM    MEM%  PIDS
 supabase_pg_meta_flashcards                 0.8%   139.4MiB    3.6%    12
 supabase_rest_flashcards                    0.2%   83.13MiB    2.1%    11
 supabase_db_flashcards                      0.0%   136.1MiB    3.5%    15

 VOLUMES (2)
 VOLUME                                         SIZE  IN USE  PROJECT
 supabase_db_flashcards                      79.11MB     yes  flashcards
 supabase_storage_flashcards                      0B     yes  flashcards

 Images 8: 6.481GB, 0B reclaimable   Volumes: 79.11MB   Build cache: 0B
 q quit   s sort (cpu / mem / name)
```

## Requirements

- macOS with Colima using the Docker runtime
- `docker` CLI
- Python 3.8+ (standard library only, no packages to install)

## Install

```bash
git clone https://github.com/nikitaWebApps/colitop.git
ln -s "$PWD/colitop/colitop" ~/.local/bin/colitop
```

Any directory on your `PATH` works in place of `~/.local/bin`.

## Usage

```bash
colitop                 # profile from $COLIMA_PROFILE, or "default"
colitop -p personal     # a specific Colima profile
colitop -c my-context   # a specific Docker context
```

| Key | Action |
| --- | --- |
| `s` | Cycle container sort: CPU, memory, name |
| `q` / `Esc` | Quit |

The Docker context defaults to `colima` for the default profile and `colima-<profile>` for named profiles, so colitop always watches Colima, whatever `DOCKER_CONTEXT` your shell has set.

Meters turn yellow above 60% and red above 85%. Container stats and VM meters refresh about every 2 seconds, volume sizes every 10 seconds. If the VM is stopped, the error is shown in place of the data and colitop recovers once the VM is back.

## License

MIT
