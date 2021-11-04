This repository contains a demo application for gamification as detailed in the article [Real-time Gaming Infrastructure for Millions of Users with Kafka, KSQL, and WebSockets](#). The folder `frontend` contains the source code of the UI. The folder `backend-deployment` contains the docker-compose file for running the Kafka, Ksqldb and MigratoryData deployment.

### How to run:

- Start Kafka, Ksqldb and Migratorydata using docker-compose.yml file from backend-deployment running command:

      docker-compose up

- Add ksql streams from file KSQL-GAMIFICATION-STREAMS.sql:

      docker exec -it ksqldb-cli ksql --file /ksql-gamification-streams/KSQL-GAMIFICATION-STREAMS.sql http://ksqldb-server:8088

- Open a browser and go to url http://localhost:8800 to open realtime gamification app.

- Publish a question using command:

      docker exec -it ksqldb-cli ksql --execute "INSERT INTO INPUT_QUESTION (id, question, answers, answer, points) VALUES ('id-1', 'How many spectators are there altogether?', ARRAY['less than 1000', 'between 1000 and 5000', 'between 5000 and 10000', 'more than 10000'], 'between 1000 and 5000', 100)" http://ksqldb-server:8088

      docker exec -it ksqldb-cli ksql --execute "INSERT INTO INPUT_QUESTION (id, question, answers, answer, points) VALUES ('id-2', 'What is the number of strokes with which this game will be won?', ARRAY['less than 10', 'between 10 and 20', 'between 20 and 30', 'more than 30'], 'more than 30', 100)" http://ksqldb-server:8088

      docker exec -it ksqldb-cli ksql --execute "INSERT INTO INPUT_QUESTION (id, question, answers, answer, points) VALUES ('id-3', 'Who will win this game?', ARRAY['Simona Halep', 'Sloane Stephens'], 'Sloane Stephens', 100)" http://ksqldb-server:8088

- Answer to the published question in the browser.
