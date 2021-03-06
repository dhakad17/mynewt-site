## <font color="#F2853F" style="font-size:24pt"> console_echo </font>

```c
void console_echo(int on)
```

Controls whether echoing is on or off for the console. When echoing is on, all characters received are transmitted back.

#### Arguments

| Arguments | Description |
|-----------|-------------|
| `on` |  1 turns on echoing, 0 turns it off  |


#### Returned values

None

#### Notes

None
              
#### Example

Here is an example where newtmgr protocol handler is controlling whether echoing is on or off. [Newtmgr](../../../newtmgr/overview.md)
turns echoing off when it is transmitting large chunks of data to a target board.

```c
static int
nmgr_def_console_echo(struct nmgr_jbuf *njb)
{
    int echo_on = 1;
    int rc;
    struct json_attr_t attrs[3] = {
        [0] = {
            .attribute = "echo",
            .type = t_integer,
            .addr.integer = &echo_on,
            .nodefault = 1
        },
        [1] = {
            .attribute = NULL
        }
    };

    rc = json_read_object(&njb->njb_buf, attrs);
    if (rc) {
        return OS_EINVAL;
    }

    if (echo_on) {
        console_echo(1);
    } else {
        console_echo(0);
    }
    return (0);
}
```

