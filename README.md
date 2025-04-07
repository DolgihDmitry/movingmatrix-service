# movingmatrix-service
The template for services based on Laravel 12 with Sail and Telescope extentions.

# Docker Compose Setup for Multi-Service Environment

This repository provides a pre-configured `docker-compose.yml` setup to quickly deploy a set of commonly used services, including **MySQL**, and **Redis**, in a local development environment. These services are essential components for database management, and caching, respectively. The configuration is designed to be flexible and extensible, allowing additional services to be easily added to the stack as needed. Each service is pre-configured with default settings, including ports, environment variables, and persistent storage mappings, making it easy to integrate into your workflow or adapt for specific project requirements.

## Prerequisites

- Docker (version 20.10 or higher)
- Docker Compose (version 3.2 or higher)

## Services Overview
### MySQL
- **Image**: `mysql:latest`
- **Ports**:
    - `3306`: MySQL port
- **Environment Variables**:
    - `MYSQL_DATABASE`: `database`
    - `MYSQL_USER`: `sail`
    - `MYSQL_PASSWORD`: `sail`
- **Volumes**:
    - Persistent data: `./mysql`

### Redis
- **Image**: `redis:latest`
- **Ports**:
    - `6379`: Redis port

### How to Use

1. **Clone the Repository**:
    `git clone https://github.com/DolgihDmitry/movingmatrix-service.git`


2. **Go to the project folder**:
   `cd movingmatrix-service`


3. **Start Services**:
   Run the following command to start all services:
   
	3.1. **Create .env file from .env-development (or copy from another similar project)**.

   	You can adjust .env file in the root of the project (if you have another settings).
  	 IMPORTANT!
   	Need to set:
   	COMPOSE_PROJECT_NAME and APP_NAME in .env file for each new service.

  	3.2. **Run create necessary folders**: 

	`mkdir -p "$PWD/storage" "$PWD/bootstrap/cache"
	mkdir -p "$PWD/storage/framework/cache/data" "$PWD/storage/framework/sessions" "$PWD/storage/framework/views"
	chmod -R 775 "$PWD/storage" "$PWD/bootstrap/cache" "$PWD/storage/framework/cache/data" "$PWD/storage/framework/sessions" "$PWD/storage/framework/views"`

 	 3.3. **Run Composer**:
		`composer install`

  	3.4. **Create Docker containers**:
		Run these in the project folder:  
		`./vendor/bin/sail build --no-cache`

 	 3.5. **Start Sail**:
		Run these in the project folder:
		`./vendor/bin/sail up -d`

  	3.6. **Check services**:
		`./vendor/bin/sail ps`

	  3.7. **Generate Laravel key**:
 		`./vendor/bin/sailartisan key:generate`

 	 3.8. **Run DB Migration**:
		`./vendor/bin/sail artisan migrate`

Notes

Update the passwords and sensitive information in the environment variables for production use.
