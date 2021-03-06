DLV Anchors
########################################

To cache a validated response for the signed zones, you need to obtain a trust and DLV anchor.

Using Putty, ssh into router01.branch01 and run the following command:

.. admonition:: TMSH

   dig dnskey dlv.isc.org.  | grep 257 > /root/DLVdnskey.txt

   dnssec-dsfromkey -f /root/DLVdnskey.txt dlv.isc.org.

.. image:: /_static/class2/dlv-cli.png

Navigate to: **DNS  ››  Caches : Cache List  ››  validating-resolver_cache : DLV Anchors**

https://router01.branch01.example.com/tmui/Control/jspmap/tmui/dns/cache/trust_anchor/list.jsp?name=%2FCommon%2Fvalidating-resolver_cache&tab=dns_cache_validating_config

.. image:: /_static/class2/dlv-add.png

For each line of output from the preceding command create a "DLV Anchor"

.. image:: /_static/class2/dlv-add-1.png

.. image:: /_static/class2/dlv-final.png

.. code-block:: tcl
   :linenos:

   tmsh modify ltm dns cache validating-resolver validating-resolver_cache dlv-anchors replace-all-with { "dlv.isc.org. IN DS 19297 5 1 7D480DBEF530374D8A4333FCB22106EB10013B46" "dlv.isc.org. IN DS 19297 5 2 A11D16F6733983E159EDF8053B2FB57B479D81A309A50EAA79A81AF48A47C617" }
