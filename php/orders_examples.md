### Orders

#### Get a list of orders from the store

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    Bigcommerce::configure(array(
    'store_url' => 'https://store-xxx.mybigcommerce.com',
    'username' => 'admin',
    'api_key' => 'xxxxxx'
    ));
    Bigcommerce_Api::setCipher('RC4-SHA')
    Bigcommerce_Api::verifyPeer(false);

    $orders = Bigcommerce::getOrders();

        foreach($orders as $order) {
            echo $order->name;
            echo $order->price;
        }
</pre>
By default, the getOrders() request returns only 50 orders. If you want to return all the orders from the store, you have to use filters. Look at the example below.

#### Create an Order
Look at <a href="https://developer.bigcommerce.com/api/orders"> orders POST </a> for a list of supported fields when creating order. Creating an order is simple -

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    Bigcommerce::configure(array(
    'store_url' => 'https://store-xxx.mybigcommerce.com',
    'username' => 'admin',
    'api_key' => 'xxxxxx'
    ));
    Bigcommerce_Api::setCipher('RC4-SHA')
    Bigcommerce_Api::verifyPeer(false);

    $createFields = array('customer_id'=>0, 'date_created' => 'Tue, 20 Nov 2012 00:00:00 +0000','status_id'=>1,'billing_address' => array( "first_name"=> "Trisha", "last_name"=> "McLaughlin", "company"=> "", "street_1"=> "12345 W Anderson Ln", "street_2"=> "", "city"=> "Austin", "state"=> "Texas", "zip"=> "78757", "country"=> "United States", "country_iso2"=> "US", "phone"=> "", "email"=> "elsie@example.com" ), "shipping_addresses" => array(), "external_source" => "POS", "products" => array() );
    
    print_r(Bigcommerce::createOrder($createFields));
</pre>

As you can see, the example shows a sample order creation, with a list of mandatory fields (billing_address, customer_id, date_created, shipping_addresses, products). You can set other fields like cost, notes, etc by simply adding to the $createFields array.

#### Get all orders from the store

Use the "limit" and "page" filter parameters to get a data beyond what the default query returns. Note that, per page, 200 orders is the max returned.

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    Bigcommerce::configure(array(
    'store_url' => 'https://store-xxx.mybigcommerce.com',
    'username' => 'admin',
    'api_key' => 'xxxxxx'
    ));
    Bigcommerce_Api::setCipher('RC4-SHA')
    Bigcommerce_Api::verifyPeer(false);

    filter = array('limit' => 200, 'page' => 1)
    $orders = Bigcommerce::getOrders(filter);

        foreach($orders as $order) {
            echo $order->name;
            echo $order->price;
        }
</pre>

In cases, when you have more than 200 orders in your store, you can use a counter to update the page, while controlling the limit parameter. You can do something like below.

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    Bigcommerce::configure(array(
    'store_url' => 'https://store-xxx.mybigcommerce.com',
    'username' => 'admin',
    'api_key' => 'xxxxxx'
    ));
    Bigcommerce_Api::setCipher('RC4-SHA')
    Bigcommerce_Api::verifyPeer(false);

    $count = Bigcommerce::getOrdersCount()/200;
    for ($i = 1; $i <= $count; $i++) {
        $filter = array('limit' => 200, 'page' => $i);
        $orders = Bigcommerce::getOrders($filter);
        foreach($orders as $order) {
            echo $order->name;
            echo $order->price;
        }
     }
    
</pre>

#### Update an order
Order takes many fields on the update requests. Refer to the documentation at http://developer.bigcommerce.com/api/orders#put-ordersidjson. Here, we update an order using just the mandatory fields.

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    Bigcommerce::configure(array(
    'store_url' => 'https://store-xxx.mybigcommerce.com',
    'username' => 'admin',
    'api_key' => 'xxxxxx'
    ));
    Bigcommerce_Api::setCipher('RC4-SHA')
    Bigcommerce_Api::verifyPeer(false);

    $order = array('status_id' => 1);
    Bigcommerce::updateOrder(110, $order);
    
</pre>


