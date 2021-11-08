## Development Steps
1. Prepare the environment.
 - [Docker](https://docs.docker.com/get-docker/)
 - [Magefile](https://magefile.org/) (v1.11 or above)
 - [Go](https://golang.org/dl/) (v1.16 or above)
 - [Node.js](https://nodejs.org/en/download/) (v14 or above)
2. Fork the project and clone it to the local system:
```bash
git clone https://github.com/YOUR_GIT_USER_NAME/tencentcloud-monitor-grafana-app.git
```
3. Install dependencies:
```bash
npm install
go mod vendor
```
4. Start the frontend development environment:
```bash
npm run watch
```
5. Start the backend development environment:
```bash
mage -v
```
6. Run the following on the command line:
```bash
docker-compose up
```
7. After completing, just visit `http://localhost:3000`.
8. After the development is completed, use a [pull request](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/pulls) to submit the code to request a merge.


## Running on Local Grafana
You can also clone this project to the local Grafana plugin directory and restart the local Grafana. Please make sure that the version of the local Grafana is at least v7.3.
