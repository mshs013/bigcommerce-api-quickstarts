### Optionsets

#### Connect options to optionsets

This is currently a four step process
1. Create the option
2. Add some values to the option
3. Create the option set
4. Create option set options using the options you just created

<pre>
    curl --request POST \
    -H "Content-Type: application/json" \
    -u "username:apikey" \
    -d '{"name":"homer simpson", "type":"T"}' \
    https://store/api/v2/options.json
</pre>

This will provide the option ID, which we will use for the next step.
<pre>
    {"id":33,"name":"homer simpson","display_name":"homer simpson","type":"T","values":{"url":"https://store-bwvr466.mybigcommerce.com/api/v2/options/33/values.json","resource":"/options/33/values"}}
</pre>

Creating a new optionset.

<pre>
    curl --request POST \
    -u "admin:key" \
    -d '{"name": "Simpson family"}' \
    -H "Content-Type: application/json" \
    https://store/api/v2/optionsets.json 
</pre>

This will provide the optionset ID, which we can use to connect the previously created option with.

<pre>
    {"id":27,"name":"Simpson family","options":{"url":"https://store-bwvr466.mybigcommerce.com/api/v2/optionsets/27/options.json","resource":"/optionsets/27/options"}}
</pre>

The final step is to connect the option with optionset

<pre>
curl --request POST \
    -u "admin:key" \
    -d '{"option_id": "33", "display_name":"Simpson family"}' \
    -H "Content-Type: application/json" \
    https://store/api/v2/optionsets/27/options.json
</pre>

Which will complete the process

<pre>
{"id":44,"option_id":33,"option_set_id":27,"display_name":"Simpson family","sort_order":0,"is_required":false,"option":{"url":"https://store-bwvr466.mybigcommerce.com/api/v2/options/33.json","resource":"/options/33"}}
</pre>



