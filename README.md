# LinkedIn Post Automation

```javascript

```

## HTTP Request
### URL:
```url
https://api.github.com/user/repos
```

## HTTP Request1
### URL:
```url
https://raw.githubusercontent.com/{{ $json.full_name }}/main/README.md
```

## AI Agent
### Prompt:
```text
You are a professional social media manager.

I just created a new GitHub repository.
Repo Name: {{ $('HTTP Request').item.json.name }}
Repo URL: {{ $('HTTP Request').item.json.html_url }}

Here is the README content:
"""
{{ $json.data }}
"""

Task:
Write a short, engaging LinkedIn post (max 150 words) to announce this project.
-Don't start with ""Here's an engaging LinkedIn post for your new project:". And simply generate the post.
- Hook: What problem does it solve?
- Tech: Briefly mention the tech stack.
- Call to Action: "Check out the code here: [Repo URL]"
- Tone: Enthusiastic but professional.
```

## HTTP Request2
### URL:
```url
https://api.linkedin.com/v2/userinfo
```

### Authorization URL:
```url
https://www.linkedin.com/oauth/v2/authorization
```

### Access Token URL:
```url
https://www.linkedin.com/oauth/v2/accessToken
```

## HTTP Request3
### URL:
```url
https://api.linkedin.com/v2/ugcPosts
```

### Body JSON:
```json
{{
  {
    "author": "urn:li:person:" + $('HTTP Request2').item.json.sub,
    "lifecycleState": "PUBLISHED",
    "specificContent": {
      "com.linkedin.ugc.ShareContent": {
        "shareCommentary": {
          "text": $('AI Agent').item.json.output
        },
        "shareMediaCategory": "NONE"
      }
    },
    "visibility": {
      "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"
    }
  }
}}
```
