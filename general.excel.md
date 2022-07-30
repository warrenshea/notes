# Warren Shea's Notes for Excel

## Compare Column A with Column B and write "Is a match" if the item in Column A is inside Column B
e.g. if Column A is a URL list, and Column B is a redirect file, and you want to find which URLs (in A) redirect.

```
=IF(ISERROR(MATCH(A1,$B$1:$B$250000,0)),"","Is a match")
```
