Bird Babel configuration
========================

In `/etc/bird/crxn/babel.conf` place the following template:

```
# CRXN Babel protocol
protocol babel crxnBabel
{

    # Interfaces to run babel on
    interface "interface1", "interface2";

    ipv6
    {
        import filter crxnFilter;
        export filter crxnFilter;
        table crxn;
    };
}
```

1. Set the `interface` list to a list of interfaces you wish the babel
protocol to run on
    * It also supports regex in a string so you can do `"interface*"` for example

**Note:** For Bird 1.6 you will want to remove the `ipv6 {};`.

And that is all!

### Additional changes

TODO: Finish this, `wired vs `wireless`

