### Optionsets

#### Connect options to optionsets

This is currently a four step process
1. Create the option
2. Add some values to the option
3. Create the option set
4. Create option set options using the options you just created

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    $option = array('name' => 'homer simpson', 'type' => 'T');
    $options = Bigcommerce::createOptions($option);
    print_r($options);
</pre>

This will provide the option ID, which we will use for the next step.
<pre>
    stdClass Object
    (
        [id] => 34
        [name] => homer simpson
        [display_name] => homer simpson
        [type] => T
        [values] => stdClass Object
            (
                [url] => https://store-bwvr466.mybigcommerce.com/api/v2/options/34/values.json
                [resource] => /options/34/values
            )

    )
</pre>

To add some values to the option add bellow function to your bigcommerce.php file after getOptionValues function
<pre>
    public static function createOptionValue($option_id, $object)
    {
        return self::createResource('/options/' . $option_id . '/values', $object);
    }
</pre>

Then create some option value
<pre>
    $optionvalue = array('label' => "Your option label", 'sort_order' => "Your option sort order", 'value' => "Your option value");
    Bigcommerce::createOptionValue('option_id',$optionvalue);
</pre>


Creating a new optionset.

<pre>
    require 'vendor/autoload.php';
    use Bigcommerce\Api\Client as Bigcommerce;

    $optionset = array('name' => 'Crazy S family');
    $osets = Bigcommerce::createOptionsets($optionset);
    print_r($osets);
</pre>

This will provide the optionset ID, which we can use to connect the previously created option with.

<pre>
    stdClass Object
    (
        [id] => 29
        [name] => Crazy S family
        [options] => stdClass Object
            (
                [url] => https://store-bwvr466.mybigcommerce.com/api/v2/optionsets/29/options.json
                [resource] => /optionsets/29/options
            )

    )
</pre>

The final step is to connect the option with optionset

<pre>
$option = array('option_id' => 34, 'display_name' => "Crazy Simpson Family");
$optionset_id = 29;
$options =  Bigcommerce::createOptionsets_Options($option,$optionset_id);
print_r($options);
</pre>

Which will complete the process

<pre>
(
    [id] => 45
    [option_id] => 34
    [option_set_id] => 29
    [display_name] => Crazy Simpson Family
    [sort_order] => 0
    [is_required] =>
    [option] => stdClass Object
        (
            [url] => https://store-bwvr466.mybigcommerce.com/api/v2/options/34.json
            [resource] => /options/34
        )

)
</pre>



