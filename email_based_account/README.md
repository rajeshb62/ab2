# Email Based Account

Create an email based aztec account. that one can sign into using an email address (gmail). and that can sign transactions from that account using apple face ID. 


## Challenge Selection
Read [this article](https://aztec.network/blog/unlocking-the-future-of-privacy-exploring-identity-and-social-use-cases-in-alpha-build-2-with-100k-in-prizes) that announces Alpha Build 2 to learn more about the challenges and get ideas on what to build!

- [x] ZKEmail Guardian
- [ ] Social Cipher

**Note**: You can change which challenges you've selected during the competition if you'd like. You are not bound by your choices or descriptions entered during the one week check-in.

## Team information

Rajesh 

## Technical Approach
### Questions/ approach
- create an account for an email address abc@xyz.com based on .eml file:
    - verify header is valid using dkim signature verification
    - check sender is 'abc@xyz.com'
    - (additional check) check if subject contains a specific random string shown in UI
- hash email into pedersen 2 hash (?), convert into field element type Fr and use it as encryption key in getSchnorrAccount(..) function and show the accoung wallet in UI (user can sign tx from this wallet as long as they know the signing key)
Inspirations: 
https://zkemail.shieldswap.org/
https://docs.aztec.network/guides/developer_guides/smart_contracts/writing_contracts/authwit#usage
Inspiration codebases: Loads account based on Face ID of user: loads account based on password: https://github.com/skaunov/aabch1_23

## Expected Outcomes
A wallet app (previously created in alpha build 1) that uses email ownership proof to create aztec account

## Lessons Learned (For Submission)

- What are the most important takeaways from your project?
- Are there any patterns or best practices that you've learned that would be useful for other projects?
- Highlight reusable code patterns, key code snippets, and best practices - what are some of the ‘lego bricks’ you’ve built, and how could someone else best use them?

## Project Links (For Submission)

Please provide links to any relevant documentation, code, or other resources that you've used in your project.

## Video Demo (For Submission)

Please provide a link to a video demo of your project. The demo should be no longer than 5 minutes and should include a brief intro to your team and your project.
