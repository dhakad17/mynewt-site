## <font color="#F2853F" style="font-size:24pt">ble\_gap\_adv\_rsp\_set\_fields</font>

```c
int
ble_gap_adv_rsp_set_fields(const struct ble_hs_adv_fields *rsp_fields)
```

### Description

Configures the data to include in subsequent scan responses.

### Parameters

| *Parameter* | *Description* |
|-------------|---------------|
| adv\_fields | Specifies the scan response data. |

### Returned values

| *Value* | *Condition* |
|---------|-------------|
| 0 | Success. |
| BLE\_HS\_EBUSY | Advertising is in progress. |
| BLE\_HS\_EMSGSIZE | The specified data is too large to fit in an advertisement. |
| [Core return code](../../ble_hs_return_codes/#return-codes-core) | Unexpected error. |
