DepSurf Dataset
===

<a href="https://depsurf.github.io">
<img src="https://depsurf.github.io/assets/logo-256.png" alt="DepSurf Logo" width="150" align="right">
</a>

Website for [EuroSys'25](https://dl.acm.org/doi/proceedings/10.1145/3689031) paper "**Revealing the Unstable Foundations of eBPF-Based Kernel Extensions**"

*Shawn (Wanxiang) Zhong, Jing Liu, Andrea Arpaci-Dusseau, and Remzi Arpaci-Dusseau*

[Paper](https://depsurf.github.io/assets/paper.pdf) |
[Code](https://github.com/ShawnZhong/DepSurf) | 
[Dataset](https://github.com/ShawnZhong/DepSurf-dataset) | 
[Website](https://depsurf.github.io/) |
[Slides](https://depsurf.github.io/assets/slides.pdf) | 
[Poster](https://depsurf.github.io/assets/poster.pdf)

<details>
<summary>
Abstract
</summary>
eBPF programs significantly enhance kernel capabilities, but encounter substantial compatibility challenges due to their deep integration with unstable kernel internals. We introduce DepSurf, a tool that identifies dependency mismatches between eBPF programs and kernel images. Our analysis of 25 kernel images spanning 8 years reveals that dependency mismatches are pervasive, stemming from kernel source code evolution, diverse configuration options, and intricate compilation processes. We apply DepSurf to 53 real-world eBPF programs, and find that 83% are impacted by dependency mismatches, underscoring the urgent need for systematic dependency analysis. By identifying these mismatches, DepSurf enables a more robust development and maintenance process for eBPF programs, enhancing their reliability across a wide range of kernels.
</details>
<details>
<summary>
Citation
</summary>

```
@inproceedings{10.1145/3689031.3717497,
  author    = {Zhong, Shawn Wanxiang and Liu, Jing and Arpaci-Dusseau, Andrea and Arpaci-Dusseau, Remzi},
  title     = {Revealing the Unstable Foundations of eBPF-Based Kernel Extensions},
  year      = {2025},
  isbn      = {9798400711961},
  publisher = {Association for Computing Machinery},
  address   = {New York, NY, USA},
  url       = {https://doi.org/10.1145/3689031.3717497},
  doi       = {10.1145/3689031.3717497},
  abstract  = {eBPF programs significantly enhance kernel capabilities, but encounter substantial compatibility challenges due to their deep integration with unstable kernel internals. We introduce DepSurf, a tool that identifies dependency mismatches between eBPF programs and kernel images. Our analysis of 25 kernel images spanning 8 years reveals that dependency mismatches are pervasive, stemming from kernel source code evolution, diverse configuration options, and intricate compilation processes. We apply DepSurf to 53 real-world eBPF programs, and find that 83\% are impacted by dependency mismatches, underscoring the urgent need for systematic dependency analysis. By identifying these mismatches, DepSurf enables a more robust development and maintenance process for eBPF programs, enhancing their reliability across a wide range of kernels.},
  booktitle = {Proceedings of the Twentieth European Conference on Computer Systems},
  pages     = {21–41},
  numpages  = {21},
  location  = {Rotterdam, Netherlands},
  series    = {EuroSys '25}
}
```

</details>

## Format

The following examples show the information available in the dataset:

- [Function status](func_groups)

```json
{
    "name": "vfs_read",
    "collision_type": "Unique Global",
    "inline_type": "Selective",
    "funcs": [
        {
            "addr": 18446744071581851376,
            "name": "vfs_read",
            "external": true,
            "loc": "fs/read_write.c:446",
            "file": "fs/read_write.c",
            "inline": "not declared, inlined",
            "caller_inline": [],
            "caller_func": [
                "fs/read_write.c:ksys_pread64",
                "fs/read_write.c:ksys_read",
                "fs/read_write.c:ksys_read",
                "fs/read_write.c:kernel_read",
                "fs/exec.c:read_code"
            ]
        }
    ],
    "symbols": [
        {
            "addr": 18446744071581851376,
            "name": "vfs_read",
            "section": ".text",
            "bind": "STB_GLOBAL",
            "size": 340
        }
    ]
}
```

- [Function type](types_func)

```json
{
    "kind": "FUNC",
    "name": "vfs_read",
    "type": {
        "kind": "FUNC_PROTO",
        "params": [
            {
                "name": "file",
                "type": {
                    "kind": "PTR",
                    "type": {
                        "kind": "STRUCT",
                        "name": "file"
                    }
                }
            },
            {
                "name": "buf",
                "type": {
                    "kind": "PTR",
                    "type": {
                        "kind": "INT",
                        "name": "char"
                    }
                }
            },
            {
                "name": "count",
                "type": {
                    "kind": "TYPEDEF",
                    "name": "size_t"
                }
            },
            {
                "name": "pos",
                "type": {
                    "kind": "PTR",
                    "type": {
                        "kind": "TYPEDEF",
                        "name": "loff_t"
                    }
                }
            }
        ],
        "ret_type": {
            "kind": "TYPEDEF",
            "name": "ssize_t"
        }
    }
}
```

- [Struct type](types_struct)

```json
{
    "kind": "STRUCT",
    "name": "mutex",
    "size": 32,
    "members": [
        {
            "name": "owner",
            "bits_offset": 0,
            "type": {
                "kind": "TYPEDEF",
                "name": "atomic_long_t"
            }
        },
        {
            "name": "wait_lock",
            "bits_offset": 64,
            "type": {
                "kind": "TYPEDEF",
                "name": "spinlock_t"
            }
        },
        {
            "name": "osq",
            "bits_offset": 96,
            "type": {
                "kind": "STRUCT",
                "name": "optimistic_spin_queue"
            }
        },
        {
            "name": "wait_list",
            "bits_offset": 128,
            "type": {
                "kind": "STRUCT",
                "name": "list_head"
            }
        }
    ]
}
```

- [Tracepoint](tracepoints)

```json
{
    "class_name": "ext4__write_begin",
    "event_name": "ext4_write_begin",
    "func_name": "trace_event_raw_event_ext4__write_begin",
    "struct_name": "trace_event_raw_ext4__write_begin",
    "fmt_str": "\"dev %d,%d ino %lu pos %lld len %u\", ((unsigned int) ((REC->dev) >> 20)), ((unsigned int) ((REC->dev) & ((1U << 20) - 1))), (unsigned long) REC->ino, REC->pos, REC->len",
    "func": {
        "kind": "FUNC",
        "name": "trace_event_raw_event_ext4__write_begin",
        "type": {
            "kind": "FUNC_PROTO",
            "params": [
                {
                    "name": "__data",
                    "type": {
                        "kind": "PTR",
                        "type": {
                            "name": "void",
                            "kind": "VOID"
                        }
                    }
                },
                {
                    "name": "inode",
                    "type": {
                        "kind": "PTR",
                        "type": {
                            "kind": "STRUCT",
                            "name": "inode"
                        }
                    }
                },
                {
                    "name": "pos",
                    "type": {
                        "kind": "TYPEDEF",
                        "name": "loff_t"
                    }
                },
                {
                    "name": "len",
                    "type": {
                        "kind": "INT",
                        "name": "unsigned int"
                    }
                }
            ],
            "ret_type": {
                "name": "void",
                "kind": "VOID"
            }
        }
    },
    "struct": {
        "kind": "STRUCT",
        "name": "trace_event_raw_ext4__write_begin",
        "size": 40,
        "members": [
            {
                "name": "ent",
                "bits_offset": 0,
                "type": {
                    "kind": "STRUCT",
                    "name": "trace_entry"
                }
            },
            {
                "name": "dev",
                "bits_offset": 64,
                "type": {
                    "kind": "TYPEDEF",
                    "name": "dev_t"
                }
            },
            {
                "name": "ino",
                "bits_offset": 128,
                "type": {
                    "kind": "TYPEDEF",
                    "name": "ino_t"
                }
            },
            {
                "name": "pos",
                "bits_offset": 192,
                "type": {
                    "kind": "TYPEDEF",
                    "name": "loff_t"
                }
            },
            {
                "name": "len",
                "bits_offset": 256,
                "type": {
                    "kind": "INT",
                    "name": "unsigned int"
                }
            },
            {
                "name": "__data",
                "bits_offset": 288,
                "type": {
                    "kind": "ARRAY",
                    "name": "(anon)",
                    "nr_elems": 0,
                    "type": {
                        "kind": "INT",
                        "name": "char"
                    }
                }
            }
        ]
    }
}
```
