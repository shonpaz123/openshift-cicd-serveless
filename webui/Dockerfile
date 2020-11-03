# Fetch the needed inage from Docker Hub
FROM node:4-slim

# Install all the needed dependencies for the application 
RUN npm install express
RUN npm install redis

# Copy the needed file into the working directory and run the application 
COPY files/ /files/
COPY webui.js /
CMD ["node", "webui.js"]

# Expose the needed port for the application 
EXPOSE 8000 
