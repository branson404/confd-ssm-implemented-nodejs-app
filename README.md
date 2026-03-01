# Todo app with Configuration mangement enabled by confd

Overview:
This project is a simple Nodejs todo-app but we implemneted confd into the app using supervisord and other yaml files that used to deploy it as a kubernetes pod and used service account to connect with AWS SSM and fetch the parameters and values from parameter store in AWS on realtime when container init it sexecuted, this make sure sure security maintains is high and threats from being entered into pods
