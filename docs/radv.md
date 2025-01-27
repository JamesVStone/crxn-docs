Radv
====

Radv or _Router advertisements_ is a feature Bird offers that can allow you to add an additional configuration to your Bird router such that you
can have it automatically configure your host devices on your CRXN /48 LAN such that they can access the LAN, the greater CRXN and also possibly
configure [CRXN DNS]() too!

---

# General syntax

You will want to add one of these to one of your Bird configuration files:

```
protocol radv
{
    # Stuff hoes here
}
```

## Advertising your prefix

If you would like to advertise your prefix to hosts on your LAN that have set their address acquisition for IPv6 to _'Automatic'_ such that they will assign themselves an address within that prefix then you will want to add a `prefix` block as so:

```
protocol radv
{
    # Advertise your prefix
    prefix fd40:ec65:5b4c::/64 {
        # TODO: Add anything that needs to be in here
    };

    # Interfaces to run radv on
    interface "eth0";

}
```

In the above example I am advertising a `/64` within my `/48`/ULA (`fd40:ec65:5b4c::/48`), `fd40:ec65:5b4c::/64`, and only on interface `eth0` will radv run.

## Advertising route(s)

You can advertise a default route, to `fd00::/8` or simply all routes in your router's routing table, to your hosts using the following:

### Advertising a single `fd00::/8`

TODO: Add this as I normally don't do this even though one should as it means less memory consumption and advertisement updates

### Advertising all known routes

This will advertise all the routes your Bird router knows (those in the `crxn` table) such that your, laptop for example, will add all of them to its routing table.

```
protocol radv
{
    # Advertise your prefix
    prefix fd40:ec65:5b4c::/64 {
        # TODO: Add anything that needs to be in here
    };

    # Interfaces to run radv on
    interface "eth0";

    # Advertise all routes (TODO: check if this is the correct syntax)
    propagate_routes yes;
    table crxn;
}
```