# ce
Common error package to wrap http error status


## Return errors

```
func (arg *CreateOrderArg) Validate() error {
	if arg.Order.ProductID == 0 {
		return ce.NewValidateError("ProductID required")
	}
	if !validate.Mobile(arg.Mobile) {
		return ce.NewValidateError("Mobile not valid")
	}
	if len(arg.Code) != 6 {
		return ce.NewValidateError("Code not valid")
	}
	return nil
}
```

## Error handling

```
if err != nil {
  if ve, ok := err.(*ce.Error); ok && ve.Unauthorized() {
    return echo.NewHTTPError(http.StatusUnauthorized, "token invalid")
  }
  return err
}
```
