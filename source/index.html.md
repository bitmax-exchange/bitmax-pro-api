---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <a href='https://bitmax.io'>BitMax.io</a>

includes:
  - auth
  - rest_pub
  - rest_pub_ticker
  - rest_pub_bar
  - rest_pub_depth
  - rest_pub_trades
  - rest_prv
  - rest_prv_bal
  - rest_prv_order
  - ws_general
  - ws_auth
  - ws_sub
  - ws_req
  - error_code

search: true
---


# BitMax Pro API Documentation

<aside class="warning">
**Important** This document is still work-in-progress and all contents are subject to change without further notice. 
</aside>

<aside class="warning">
**Important** APIs in this document are not yet available for public access.
</aside>

BitMax Pro API is the latest release of APIs allowing our users to access the exchange programmatically. It is a major revision 
of the older releases. The BitMax team re-implemented the entire backend system in support for the BitMax Pro API. It is designed
to be fast, flexible, stable, and comprehensive. 

### What's New

* Dynamic subscription/unsubscription to private and public data channels via WebSocket. 
* Synchronized/Asynchronized API calls. When placing/cancelling orders, you may use synchronized method 
  to get the order result in a single API call. You may also use asynchronized method to achieve minimum latency. 
* Simplified API schemas. For instance, we simplified the cancel order logic, now you can track the entire order
  life cycle with only one indentifier (`orderId`). 

### Demo codes

We provide comprehensive demos (currently available in python). We provide two types of demo codes:

* Short, self contained demo scripts that you can plugin to you larger system. 
* Large, complex demo scripts to show you how to design a trading strategy using APIs from this document.

See [https://github.com/bitmax-exchange/bitmax-pro-api-demo](https://github.com/bitmax-exchange/bitmax-pro-api-demo) for more details.
