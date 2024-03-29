# Cross-Origin Resource Sharing (CORS)

In the vast landscape of web development, imagine you're hosting a party at your home. You have your friends coming over, bringing snacks, drinks, and music. Everything's set for a great time.

Now, let's say your neighbor, who lives across the street, decides to join the party. They knock on your door and ask to join in on the fun. Here's where things get interesting: just like your browser does with web pages, you need to decide whether to let your neighbor join the party.

## What is CORS?

Cross-Origin Resource Sharing (CORS) is like your house party's guest list. It's a security feature that controls which guests (or web pages) are allowed to access resources (like data or images) on your website from other origins (or domains).

## Why is CORS Necessary?

Without CORS, web browsers follow a same-origin policy, which means they only allow web pages to request resources from the same origin (or domain) as the page itself. This policy helps prevent unauthorized access to sensitive data.

But what if you want to share some snacks or drinks with your neighbor? That's where CORS comes in. It allows your website to specify which origins are permitted to access its resources, expanding the guest list to include trusted neighbors while keeping out unwanted guests.

## Example of CORS in Action

Imagine you have a website (let's call it "example.com") that hosts some photos. Your friend's website ("friend.com") wants to display one of these photos on their page. When their web page requests the photo from your website, the browser checks if your website allows requests from "friend.com" using CORS.

If your website has CORS configured to allow requests from "friend.com," the browser serves up the photo without any issues, just like you would welcome your friend to your house party. But if CORS is not configured to allow requests from "friend.com," the browser will block the request, just like you would politely decline entry to an uninvited guest at your party.



## Conclusion

In summary, CORS acts like a bouncer at a party, deciding which guests (or web pages) are allowed to access resources (like photos or data) on your website from other origins (or domains). By configuring CORS properly, you can ensure that your website stays secure while still allowing trusted neighbors to join in on the fun.

[NEXT DOC: Access Control Rules in CORS](access-control-cors.md)