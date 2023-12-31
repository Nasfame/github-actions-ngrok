# Github Actions Ngrok Tunnel

[![GitHub stars](https://img.shields.io/github/stars/Nasfame/github-actions-ngrok)](https://github.com/durgeshsamariya/awesome-github-profile-readme-templates/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Nasfame/github-actions-ngrok?color=blue)](https://github.com/durgeshsamariya/awesome-github-profile-readme-templates/network)
[![GitHub contributors](https://img.shields.io/github/contributors/Nasfame/github-actions-ngrok?color=blue)](https://github.com/durgeshsamariya/awesome-github-profile-readme-templates/network)


This action is based on [this repository](https://github.com/Nasfame/github-actions-ngrok).

This is a Github Action that can be used in your Github Workflow to tunnel incoming/outgoing TCP or HTTP traffic in your workflow environment, achieving temporary deployment for testing or other purposes.

## How to use

This action accepts the following parameters:

| Name| Description | Required  | Default |
| ------------- |-------------|-----|-----|
| timeout | After this timeout the deployment will automatically shutdown the tunelling and therefore stop the action. (max is 6 hours) | No | 1h |
| port | The port in localhost to forward traffic from/to  | Yes | - |
| ngrok_authtoken | Your ngrok authtoken| Yes | - |
| tunnel_type | Whether the tunnel type will be TCP or HTTP | Yes | tcp |
| save_url_to_filename | If provided, save the deployed tunnel's URL to a file with the provided name, otherwise just print URL on console | No | - |


Here is an example of using this action:

```yaml
name: CI
on: push

jobs:

  deploy:
    name: Docker container with Ngrok tunnel
    runs-on: ubuntu-latest
    needs: cancel

    steps:
    - name: Checkout
      uses: actions/checkout@v2
    
    - name: Run container
      run: docker-compose up -d 
    
    - uses: Nasfame/github-actions-ngrok@<VERSION>
      with:
        timeout: 1h
        port: 8080
        ngrok_authtoken: ${{ secrets.NGROK_AUTHTOKEN }}
        tunnel_type: http
        save_url_to_filename: tunnelURL.md
```
