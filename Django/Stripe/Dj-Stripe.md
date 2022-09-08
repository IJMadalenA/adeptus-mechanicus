# Dj-Stripe



## Comandos esenciales. 

Sincronizar toda la base de datos local.

```python
>>> python manage.py djstripe_sync_models
```

https://dj-stripe.dev/usage/manually_syncing_with_stripe/



## Modelos.

```mermaid
classDiagram

class StripeBaseModel
StripeBaseModel : djstripe_created
StripeBaseModel : djstripe_updated


class StripeModel
StripeModel : djstripe_id
StripeModel : id
StripeModel : Account
StripeModel : livemode
StripeModel : created
StripeModel : metadata
StripeModel : description

StripeModel : human_readable_amount(self) str
StripeModel : _get_stripe_account_id(self, api_key)


class Product
Product : name - str
Product : type - int
Product : active - bool
Product : attributes - JSON
Product : caption - str
Product : deactivate_on - JSON
Product : images - JSON
Product : package_dimensions - JSON
Product : shippable - bool
Product : url - str
Product : statement_description - str
Product : unit_label - str

class Customer
Customer : adderss - JSON
Customer : balance - int
Customer : currency - str
Customer : default_source - FK
Customer : delinquent - bool
Customer : deleted - bool
Customer : coupon_start - date
Customer : coupon_end - date
Customer : email - str
Customer : invoice_prefix - str
Customer : invoice_settings - JSON
Customer : default_payment_method - FK
Customer : name - str
Customer : phone - str
Customer : preferred_locales - JSON
Customer : shipping - JSON
Customer : tax_exempt - str
Customer : subscriber - FK
Customer : date_purged - date

Customer : _manipulate_stripe_object_hook()
Customer : get_or_create()
Customer : create()
Customer : credits()
Customer : customer_payment_methods()
Customer : pending_charges()
Customer : subscribe()
Customer : charge()
Customer : add_invoice_item()
Customer : add_card()
Customer : add_payment_method()
Customer : purge()
Customer : _get_valid_subscriptions()
Customer : is_subscripbed_to()
Customer : has_any_active_subscription()
Customer : active_subscriptions()
Customer : valid_subscriptions
Customer : subscription()
Customer : can_charge()
Customer : send_invoice()
Customer : retry_unpaid_invoice()
Customer : add_coupon()
Customer : upcoming_invoice()
Customer : _attach_objects_post_save_hook()
Customer : _attach_objects_hook()
Customer : _sync_invoices()
Customer : _sync_charges()
Customer : _sync_cards()
Customer : _sync_subscriptions()


class PaymentIntent
%%     """
%%    Stripe documentation: https://stripe.com/docs/api#payment_intents
%%    """
PaymentIntent : amount - int
PaymentIntent : amount_capturable - int
PaymentIntent : amount_received - int
PaymentIntent : canceled_at - date
PaymentIntent : cancellation_reason - int
PaymentIntent : capture_method - int
PaymentIntent : client_secret - str
PaymentIntent : confirmation_method - str
PaymentIntent : currency - str
PaymentIntent : customer - FK
PaymentIntent : description - str
PaymentIntent : last_payment_error - JSON
PaymentIntent : next_action - JSON
PaymentIntent : on_behalf_of - FK<Account>
PaymentIntent : payment_method - FK<PaymentMethod>
PaymentIntent : payment_method_types - str
PaymentIntent : receipt_email - str
PaymentIntent : setup_future_usage - str
PaymentIntent : shipping - JSON
PaymentIntent : statement_descriptor - str
PaymentIntent : status - str
PaymentIntent : transfer_data - JSON
PaymentIntent : transfer_group - str

PaymentIntent : update()
PaymentIntent : _api_cancel()
PaymentIntent : _api_confirm()


class Price
 %% """
 %%     Prices define the unit cost, currency, and (optional) billing cycle for
 %%     both recurring and one-time purchases of products.
 %% 
 %%     Price and Plan objects are the same, but use a different representation.
 %%     Creating a recurring Price in Stripe also makes a Plan available, and vice versa.
 %%     This is not the case for a Price with interval=one_time.
 %% 
 %%     Price objects are a more recent API representation, support more features
 %%     and its usage is encouraged instead of Plan objects.
 %% 
 %%     Stripe documentation:
 %%     - https://stripe.com/docs/api/prices
 %%     - https://stripe.com/docs/billing/prices-guide
 %%     """
Price : active - bool
Price : currency - str
Price : nickname - str
Price : product - FK<Product>
Price : recurring - JSON
Price : type - str
Price : unit_amount - int
Price : unit_amount_decimal - int
Price : billing_scheme - int
Price : lookup_key - str
Price : tiers - JSON
Price : tiers_mode
Price : transform_quantity - JSON

Price : get_or_create()
Price : create()
Price : human_readable_price()



StripeModel <-- StripeBaseModel

%% Refund <-- StripeModel
Price <-- StripeModel
%% Payout <-- StripeModel
%% SetupIntent <-- StripeModel
PaymentIntent <-- StripeModel
%% FileLink <-- StripeModel
%% File <-- StripeModel
%% Event <-- StripeModel
%% Dispute <-- StripeModel
Customer <-- StripeModel
Product <-- StripeModel
%% Mandate <-- StripeModel
%%  Charge <-- StripeModel
%% BalanceTransaction <-- StripeModel

```

Ciertos modelos contienen campos especiales definidos en la siguiente carpeta de la librería:

```shell
/venv/lib/python3.8/site-packages/djstripe/fields.py
```