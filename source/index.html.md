---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <a href='https://bitmax.io'>BitMax.io</a>

includes:
  - rest_general
  - rest_auth
  - rest_pub
  - rest_pub_assets
  - rest_pub_products
  - rest_pub_ticker
  - rest_pub_bar
  - rest_pub_depth
  - rest_pub_trades
  - rest_act
  - rest_act_info
  - rest_act_fee
  - rest_prv_bal
  - rest_prv_order
  - rest_prv_order_new
  - rest_prv_order_cancel
  - rest_prv_order_cancel_all
  - rest_prv_order_new_batch
  - rest_prv_order_cancel_batch
  - rest_prv_order_query
  - rest_prv_order_open
  - rest_prv_order_hist_curr
  - ws_general
  - ws_keep_alive
  - ws_auth
  - ws_sub
  - ws_sub_level1
  - ws_sub_level2
  - ws_sub_trades
  - ws_sub_bar
  - ws_sub_order
  - ws_req
  - ws_req_level2
  - ws_req_order_place
  - ws_req_order_cancel
  - ws_req_order_cancel_all
  - ws_req_order_open
  - ws_req_trades
  - error_code

header_navigators:
  - <a href="https://github.com/bitmax-exchange/bitmax-pro-api" class="current">BitMax Cash/Margin APIs</a>
  - <a href="https://github.com/bitmax-exchange/bitmax-futures-api-doc">Futures APIs</a>

search: true
---


# BitMax Pro API Documentation

BitMax Pro API is the latest release of APIs allowing our users to access the exchange programmatically. It is a major revision 
of the older releases. The BitMax team re-implemented the entire backend system in support for the BitMax Pro API. It is designed
to be fast, flexible, stable, and comprehensive. 

## What's New

* Dynamic subscription/unsubscription to private and public data channels via WebSocket. 
* Synchronized/Asynchronized API calls. When placing/cancelling orders, you may use synchronized method 
  to get the order result in a single API call. You may also use asynchronized method to achieve minimum latency. 
* Simplified API schemas. For instance, we simplified the cancel order logic, now you can track the entire order
  life cycle with only one indentifier (`orderId`). 
* More detailed error message.

## Demo codes

We provide comprehensive demos (currently available in python). We provide two types of demo codes:

* Short, self contained demo scripts that you can plugin to you larger system. 
* Large, complex demo scripts to show you how to design a trading strategy using APIs from this document.

See [https://github.com/bitmax-exchange/bitmax-pro-api-demo](https://github.com/bitmax-exchange/bitmax-pro-api-demo) for more details.


## Release Note 

**2019-12-26**

* Added execution instruction to order messages (place new order, list open/historical orders). This field indicates if the order is Post-Only (`Post`) or forced liquidation (`Liquidation`). It is named `execInst` 
  in RESTful responses and `ei` in websocket messages. 

