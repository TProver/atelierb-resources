# Troubleshooting

## Table of Contents

- [Unable to run User Pass](#unable-to-run-user-pass)

## Unable to run User Pass (4.7)

It appears that some interactive demonstrations elaborated with Atelier B 4.5 (or older) are not replaying with Atelier B 4.7.
Indeed the PO generator has been corrected and its behaviour is not exactly the same between 4.5 and 4.7:
- the number of POs is slightly different. 
- identifiers were postfixed with $1, $2, etc. to discriminate abstract variable or intermediate values in the implementation. This postfixing is now not present if not required. So an interactive proof command using one postfixed variable (like ah(xx$1=0)) is not going to be successful and the demonstration is likely to fail when replayed.
- Functional and well-definess proof obligations are now stored in the same file. POs related to functional coherency have their name prefixed with Operation\_. POs related to well-definess have their name prefixed with WellDenidness\_.

The workaround is to modify manually your pmm files (THEORY User_Pass):
- add Operation\_ or WellDefineness\_ to your Operation filter
- replace identifier$i by identifier in your proof commands if identifier$i doesn't appear any more in the PO (where i is an integer)

For example:
```
THEORY User_Pass IS
Operation(query_membership) & ff(0) & eh(member,_h,Goal) & pp(rt.1 | 60)
END
```
has to be rewritten in
```
THEORY User_Pass IS
Operation(Operation_query_membership) & ff(0) & eh(member,_h,Goal) & pp(rt.1 | 60)
END
```