Download Link: https://assignmentchef.com/product/solved-csci1100-computer-science-1-homework-9-dictionaries-and-classes
<br>
<h1>Part 1: Yelp Business Categories (40 points)</h1>

This first part revisits our Yelp exercise in a different way using a JSON formatted file. JSON was briefly covered in Lecture 13, but you should be able to figure it out based on the following. To begin, you are given the actual Yelp database from Lab 5 in JSON form in a file called businesses.json. Each line of the file is a JSON formatted string corresponding to a business. For example, the following program will read and print some of the information for the business represented on the first line of the file:

import json f = open(<sup>’</sup>businesses.json<sup>’</sup>) line = f.readline() business = json.loads(line) print(business[<sup>’</sup>name<sup>’</sup>]) print(business[<sup>’</sup>categories<sup>’</sup>])

Excuting it will result in the following output<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>:

Mustang BBQ

[u<sup>’</sup>Food<sup>’</sup>, u<sup>’</sup>Specialty Food<sup>’</sup>, u<sup>’</sup>Meat Shops<sup>’</sup>, u<sup>’</sup>Barbeque<sup>’</sup>, u<sup>’</sup>Restaurants<sup>’</sup>]

The function call json.loads(line) turns the JSON line into a dictionary with a number of entries. You can see all the dictionary entries for this first business by adding a for loop to the above code to loop through the keys and print the key and the values. All of the keys are strings, but the values are booleans, integers, floats, lists and strings! For example, for the key categories, shown in the output above, the value is a list of “Unicode” strings — strings that can handle many different language character encodings. This is nothing that you need to worry about here because you can just treat them like regular strings.

Write a program that reads a category name (correctly spelled) and a cutoff value (a valid integer). Your program must scan through the businesses — remember there is one business per line — and determine the counts for all categories that co-occur with the given category. It should then print those categories with counts greater than the given cutoff in sorted order. Right align the category names to 30 characters. (Remind yourself what the string function rjust does.) For example, after processing the above business, we will find that categories

‘Food’,’Specialty Food’,’Meat Shops’,’Barbeque’ have occurred once. You will update the counts as you find more occurrences of a list containing the input category!

Here are some possible runs of your program:

Enter a category ==&gt; Food

Food

Cutoff for displaying categories =&gt; 5

5

Categories co-occurring with Food:

Grocery: 5

Ice Cream &amp; Frozen Yogurt: 6

Restaurants: 8

Enter a category ==&gt; Restaurants

Restaurants

Cutoff for displaying categories =&gt; 4

4

Categories co-occurring with Restaurants:

American (Traditional): 4

Breakfast &amp; Brunch: 4

Chinese: 6

Delis: 4

Food: 8

Pizza: 17

Sandwiches: 4

Seafood: 4

Note: interestingly, not all Restaurants are considered Food and more restaurants are considered Pizza than Food! Here is one more example.

Enter a category ==&gt; Shopping

Shopping

Cutoff for displaying categories =&gt; 2

2

Categories co-occurring with Shopping:

Books, Mags, Music and Video: 3

Comic Books: 2

Home &amp; Garden: 2

Jewelry: 2

If the requested category is not found, your program must print Requested category is not found. If there are no categories to print (none co-occurring or none above the cutoff), your program must print None above the cutoff. See example runs below.

Enter a category ==&gt; restaurants restaurants

Cutoff for displaying categories =&gt; 4

4

Requested category is not found

Enter a category ==&gt; Shopping

Shopping

Cutoff for displaying categories =&gt; 5

5

Categories co-occurring with Shopping:

None above the cutoff

<h1>Part 2: Yelp Business Reviews (40 points)</h1>

In this part, we will use two files. The first one is the file called businesses.json described in Part 1. Note that each business has a ‘business_id’ that uniquely identifies that business. Two businesses may have the same name, corresponding to the different stores in different locations, but they will still have different ‘business_id’ values. For example, in the file given to you, you have two different stores for “Hannaford Supermarkets” with ‘business_id’ values: ‘UZFBK4pU-VcEt1N4IoYCRA’ and ‘LO0TfAyhOYR8fVuido_9aA’.

In addition to this, you are given a second file called reviews.json. This file contains one review for a business in each line. You are only interested in the review text and the ‘business_id’ for each review. For example, the following program will read and print the review for the first line of the file:

import json f = open(<sup>’</sup>reviews.json<sup>’</sup>) line = f.readline() review = json.loads(line) print(review[<sup>’</sup>business_id<sup>’</sup>]) print()

print(review[<sup>’</sup>text<sup>’</sup>])

will result in the following output:

gekPL0Kc7w9zLDT3EulvxQ

Great fish fry. The fish is fresh and comes in a great portion size. Service is good. Having left the area, I really miss this place.

Note that the review will appear on a single line. The line break in this document is just an artifact of the line being too long to fit on the page.

Write a program that reads the name of a business using input and finds the reviews for a <strong>single </strong>store of the given business. For businesses with only one location, you can just use the single <strong>business id </strong>to access the reviews file. For businesses with more than one location, you must give the user the addresses of the various locations and let them select which one to use. Validate the input to make sure that the user choice is in the range of available locations. Once you have a single store, your program must print the reviews for that store in the order they are found in the file, formatted with four spaces on the left and broken into lines using the textwrap module. Note that to get the required review format, you will need something like the following:

import textwrap wrapper = textwrap.TextWrapper( initial_indent = ‘ ‘*4, subsequent_indent = ‘ ‘*4 ) lines = wrapper.wrap(review_text)

The rest you’ll have to figure out yourself. Use the default textwidth. Note: textwrap will remove newline characters. In this input data, paragraph breaks are indicated by two consecutive newline characters. Make sure you print one blank line between paragraphs in a review. If the business requested is not found, print a message (see below). If no review is found for the given business, print a message (see below).

Example runs are given below.

Enter a business name =&gt; Bombers Burrito Bar

Bombers Burrito Bar

This business is not found

Enter a business name =&gt; Rensselaer Polytechnic Institute

Rensselaer Polytechnic Institute

Using Rensselaer Polytechnic Institute at:

110 8th St

Ste 2

Troy, NY 12180

No reviews for this business are found

Enter a business name =&gt; Country True Value Hardware

Country True Value Hardware

Using Country True Value Hardware at:

217 N Greenbush Rd

Troy, NY 12180

Review: 1

Best customer service, and they have everything.

Review: 2

This is my one stop shop for most of my basic hardware and home and garden needs because I<sup>’</sup>m in and out of here in no time.

There<sup>’</sup>s enough parking around the building, which is close to the front door. Country True Value is not the cheapest pricewise, but most items are convenient for me to find. The employees are easy to track down and are very helpful in locating items in the store when I need them.

Earlier this month, I ended up buying my grass seed here instead of at Home Depot because I couldn<sup>’</sup>t wait around for the Home Depot employee to use the forklift while it was pouring rain outside. Of course, I paid a little more here for the convenience.

Sometimes smaller is better!

Finally, note that the business below has multiple stores. You need to ask for which location to use and then print the reviews for only that location:

Enter a business name =&gt; Ted<sup>’</sup>s Fish Fry

Ted<sup>’</sup>s Fish Fry Found Ted<sup>’</sup>s Fish Fry at:

1.

700 Hoosick Rd

Troy, NY 12180

2.

636 New Loudon Rd

Ste 2

Latham, NY 12110

3.

447 3rd Ave

Watervliet, NY 12189

Select one from 1 – 3 ==&gt; 0

0

Select one from 1 – 3 ==&gt; 4

4

Select one from 1 – 3 ==&gt; 2

2

Using Ted<sup>’</sup>s Fish Fry at:

636 New Loudon Rd

Ste 2

Latham, NY 12110

Review: 1

Ted<sup>’</sup>s Fish Fry now has an official website and a Facebook page! Congrats on almost 60 years in business!

They have some very cool photos on both, hehe :-O

WEBSITE: http://www.tedsfishfry.net

FACEBOOK: http://www.facebook.com/pages/Watervliet-NY/Teds-FishFry/240983270362

Review: 2

3 stars is just about right. The fish frys are very good, although I didn<sup>’</sup>t like their chili sauce…it was more like relish, but there were a lot of regular customers ordering it so ymmv. Had a fish fry with cocktail sauce and tartar that was very good. The staff here just yell the food back to the kitchen help and they are always getting it screwed up or miscommunicated…comical, maybe that is part of the charm? I also had a hot dog and the sauce is sort of bland…I prefer hot dog sauce with a lot more flavor and kick. They also had carrot cake and cheesecake available…figured they had to be great…the carrot cake was a little dry. Go eat fish frys, figure out what you like on them and you will be good to go.

<h1>Part 3: Capturing a Pokemon (40 points)</h1>

We’ve been dealing with pokemon by walking around a grid and searching. In this part, you will implement a simple game revolving around throwing pokeballs at pokemon instead. To simplify the program, the list of all pokemon and all player moves are given in a single file. You can assume that all input from the file is valid. Your program must read the name of the file using input.

The first line of the file tells you how many pokemon there are. This is followed by the description of each pokemon, and then all the player moves. Read the pokemon first and print out the pokemon you created in the order they were in the file, then perform all player moves until either there are no more moves (the players are out of pokeballs), or all pokemon are captured.

Your program must define and use a class called Pokemon that stores relevant information about each pokemon. Define the class in the same file as the main code to simplify submission. Each pokemon has the following information:

Name|x|y|radius|health

Each pokemon is a circle with center at x,y and with radius radius. The health defines how many hits it takes to capture this pokemon. Good news: pokemon don’t move. Even better news: all players take aim at the same set of pokemon for simplicity.

A player move is given by:

Player Name|x|y which means that a player with the given name has thrown a pokeball at the coordinates (x,y). Balls are thrown by players in the order they are shown in the file. Pokeballs have an area of effect of radius 5, but they are most effective when they actually hit the pokemon. If the pokeball hits the pokemon (the distance between where the pokeball was thrown to and the pokemon location is <strong>less than </strong>the radius of the pokemon), the pokemon loses 2 health. If the pokeball doesn’t hit the pokemon, but the pokemon is within the area of effect (the distance between where the pokeball was thrown to and the pokemon location is <strong>less than </strong>the radius of the pokemon + 5), the pokemon loses one health. Health cannot go below 0. Any pokemon whose health goes to 0 is captured by the player that threw the last pokeball.

Each time a player throws a pokeball that affects a pokemon, display a message. If the player misses completely, display a message as well. If a pokemon is caught – display a message. Keep track of which pokemon each player catches. A player cannot hit a captured pokemon. A pokeball can only hit or affect one pokemon in a turn. When printing pokemon names, right justify them 12 characters.

Anytime a player captures the last pokemon, or the players run out of pokeballs, the game ends. Print a message indicating the end and print out an alphabetic listing of the players and how many pokemon they caught.

<h1>Order of Play</h1>

Here is a quick summary of the order of play:

<ol>

 <li>Read in the number of pokemon and create a list of each of the pokemon in the file</li>

 <li>Print out a summary of the pokemon found. Pokemon names should be right justified 12 spaces</li>

 <li>Execute all of the player moves in the file until there are no more, or until all pokemon are caught</li>

 <li>Print a message when a pokemon is hit by a pokeball regardless of if it is a direct hit, or if the pokemon is just within the area of effect</li>

 <li>Print a message if a pokeball completely misses</li>

 <li>Print a message if a pokemon is captured</li>

 <li>At the end, print a message, followed by an alphabetic listing of the players and the pokemon they caught. Again pokemon names should be right justified 12 spaces</li>

</ol>

We have provided two sample inputs and outputs in the ZIP file for this homework.


