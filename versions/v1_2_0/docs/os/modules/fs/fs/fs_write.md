## <font color="#F2853F" style="font-size:24pt">fs\_write</font>

```c
int fs_write(struct fs_file *file, const void *data, int len)
```

Writes the supplied data to the current offset of the specified file handle.  

#### Arguments

| *Argument* | *Description* |
|-----------|-------------|
| file |  Pointer to the file to write to |
| data |  The data to write |
| len | The number of bytes to write |


#### Returned values

* 0 on success
* [FS error code](fs_return_codes.md) on failure

#### Notes 

For files opened in append mode, the specified data is always written to the end.

#### Header file

```c
#include "fs/fs.h"
```

#### Example

```c
int
write_config(void)
{
    struct fs_file *file;
    int rc;

    /* If the file doesn't exist, create it.  If it does exist, truncate it to
     * zero bytes.
     */
    rc = fs_open("/settings/config.txt", FS_ACCESS_WRITE | FS_ACCESS_TRUNCATE,
                 &file);
    if (rc == 0) {
        /* Write 5 bytes of data to the file. */
        rc = fs_write(file, "hello", 5);
        if (rc == 0) {
            /* The file should now contain exactly five bytes. */
            assert(fs_filelen(file) == 5);
        }

        /* Close the file. */
        fs_close(file);
    }

    return rc == 0 ? 0 : -1;
}
```
