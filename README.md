
## Customer Scenario
- Security team needs help for proper reviews to code being added into our repositories. 
- Client has hundreds of repositories in the organization. 
- Need a solution that can accomplish this at scale. 


## WebHook
- Can be configured programmatically via GitHub API
- Requires a web server that listens to the request from GitHub
- If nothing is listening, GitHub will attempt to connect to the server and eventually timeout
- Needs an address on the Internet that GitHub can reach
- Localhost won’t work as other computer can’t resolve to localhost

## ngrok
- Create a public address that you can send webhooks to
- Forward those requests to your machine

## Solution
- When a new repository is created, an organization event is published.
- Automate repository branch protection by using a web service listening for organization events. 
- Web service notifies developer @mention in the repository that the protections were added.

## Tools
- Python 2
- Flash
- ngrok

## Steps
- Set GH_TOKEN as an env variable
- Set user value in app.py
- Start local web service with flash run –host=0.0.0.0 &
- Start forwarding service with ./ngrok http 5000 &
- Set forwarding address in the output of the ngrok application

## Flow
- Set up a web hook in the new GitHub organization
- Set the payload URL to match the forwarding address from ngrok
- Configure organization event to check for new repository
- Save the Web Hook configuration

## Testing
- Create a new repository
- Validate that the branch protection and an issue was created

## Future Steps
- Explore Azure Functions
- Payload max size at 25 MB. If the organization event has a large payload, webhook may not get fired.
- Size of the payload tie to the number of branches and tags that were created 
- Set up monitoring on events and payload
- Delay in code for main branch creation


