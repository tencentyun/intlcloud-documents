## Development Steps
1. Prepare the environment.
- [Docker](https://docs.docker.com/get-docker/)
- [Magefile](https://magefile.org/) >= 1.11
- [Go](https://golang.org/dl/) >=1.16
- [Node.js](https://nodejs.org/en/download/) >= 14
2. Fork the project and clone it to the local system:
```bash
$ git clone https://github.com/${your-git-username}/tencentcloud-monitor-grafana-app.git
```3. Install dependencies:
```bash
$ npm install
$ go mod vendor
```4. Start the frontend development environment:
```bash
$ npm run watch
```5. Start the backend development environment:
```bash
$ mage -v
```6. Run the following in the CLI:
```bash
$ docker-compose up
```Then visit `http://localhost:3000`.
7. After the development is completed, use a [pull request](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/pulls) to submit the code to request a merge.


## Running on Local Grafana
You can also clone this project to the local Grafana plugin directory and restart the local Grafana. Please make sure that the version of the local Grafana is above 7.0.
