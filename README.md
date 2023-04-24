# GithubActionForJira

# Find Jira tickets from git logs (commit message + description)
### required git checkout with fetch-depth: 0
### inputs
- ticket_regex : regex to find

### outputs
- jira_tickets ($GITHUB_ENV)

### sample
```
# Required git checkout with 'fetch-depth: 0'
- name: Checkout code
  uses: actions/checkout@v3
  with:
    fetch-depth: 0 
    token: ${{ secrets.GITHUB_TOKEN }}
  
- name: Find Jira tickets in commit messages and descriptions
  id: find_tickets
  uses: iplepine/GithubActionForJira/find-jira-tickets@v1
  with:
    ticket_regex: '[a-z]{2,}-\d+'
```



# Update Jira tickets
### inputs
- jira_api_token: "Jira API token" (same user with email)
- jira_email: "Jira email" (same user with token)
- jira_instance_url: "Jira instance URL" (ex. "https://<your-company>.atlassian.net")
- jira_tickets: "List of Jira tickets with white space" (ex. "KMA-111 KMA-333 Kma-391")
- jira_update_field: "Jira field ID" (ex. customfield_10101)
- jira_update_field_value: "jira field value"


# Sample Useage
```
- name: Update Jira Tickets
  uses: iplepine/GithubActionForJira/update-jira-tickets@v1
  with:
    jira_email: ${{ secrets.JIRA_EMAIL }}
    jira_api_token: ${{ secrets.JIRA_API_TOKEN }}
    jira_instance_url: ${{ secrets.JIRA_INSTANCE_URL }}
    jira_tickets: ${{ env.jira_tickets }}   # saved from find-jira-tickets
    jira_update_field: "customfield_11010"
    jira_update_field_value: "field value what you want"

```
