# Simple Etsy listings to Jekyll scripts

These are really simple Ruby scripts to get the details of all the listings in an Etsy store and save them in Jekyll-friendly formats. The first script saves the details to a YAML file, while the second saves the details to a custom collection.

## How to use

You need Ruby on your computer for this.

Go to https://www.etsy.com/developers/ and create a new app.

In the script file, replace YOUR_API_KEY with your app's keystring, and YOUR_SHOP_ID with the id of the shop you want to get the listings for. The Etsy API is rate limited, so change the rateLimit value to the number of listings in the shop.

Etsy listing titles tend to be more optimised for search than for humans, so I've added an option to trim the title at the first instance of a character. I separate the title from keywords in my listings by using a pipe symbol '|', but you can change it to whatever you want by editing the stopChar variable. Both the full title and the trimmed title are available for you to use later.

It's only able to get listings in batches of 100, so you'll need to include the offset number as an argument in the command. For example to get listings 0-100 the offset is 0, for 100-200 the offset is 100 etc.

cd to the script file in Terminal and run it by typing ```ruby listing-to-collection.rb [offset]```.

## How it works

The script works in two stages. Firstly it gets all the data associated with a listing, then, as images are handled by Etsy separately, it looks up the image info for each. It's able to get all images. 

Although the API call first returns all of the data associated with a listing as a JSON object, the script doesn't print everything - I only needed a few fields. If you need a field which currently isn't there, it's straightforward to add. 

Look at the listing API reference page https://www.etsy.com/developers/documentation/reference/listing#section_fields and pick your field. Then add a new line to the script, after line 30, like this:

```ruby
file.puts "  FIELD_TITLE: #{listing["FIELD"]}"
```

FIELD_TITLE is what you want to call the field in the YAML file. FIELD is the name of the Etsy field (they can have the same name). So, to print the description field, you'd write:

```ruby
file.puts "  description: #{listing["description"]}"
```


