###########################
Build Swagger API Reference
###########################

To build Swagger API reference:

	#. Clone the `swagger <https://github.com/MaterialDev/swagger>`_ git repo
	#. Clone the `swagger-ui <https://github.com/MaterialDev/swagger-ui>`_ git repo
	#. Navigate to local swagger repo
		
		#. ``npm install``
		#. ``gulp``

	#. Edit index.html in swagger-ui\src\main\html and add "material.api.json" to the URL location around line 54\
	#. Copy material.api.json from swagger\dist to swagger-ui\src\main\html
	#. Navigate to local swagger-ui repo

		#. ``npm install``
		#. ``gulp``
		#. ``gulp serve``
		#. Ctrl+C to stop server
		#. Navigate to localhost:8080 in browser


