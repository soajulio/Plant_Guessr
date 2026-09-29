# Plant Recognition Project  

This french project is divided into two repositories available on my GitHub:  

1. **Frontend**: React Native application for plant identification → [Anclin_Soares_SAE_Front](https://github.com/soajulio/Anclin_Soares_SAE_Front)  
2. **Backend**: Flask API with PostgreSQL database → [Anclin_Soares_SAE_Back](https://github.com/soajulio/Anclin_Soares_SAE_Back)  

Both repositories contain full commit history.  

## Team  

Built as a two-person university project by **Ethan Anclin** and **Julio Soares**.  

## Technologies Used  

- **Frontend**: React Native, Axios, React Navigation  
- **Backend**: Flask (Python), PostgreSQL, Docker  
- **APIs**: Plant.id for plant recognition  

## Getting Started  

This repository contains two folders:  

- `Front/` → React Native project  
- `Back/` → Flask backend  

Follow the **readme** inside each folder to install dependencies and run the project (in french).

## Known Limitations & Security  

This is a university project built to run on a local network for a demo. It is **not production-ready**. A security review of the code found these issues:  

- **No real authentication**: the API has no session or token and trusts the `user_id` the client sends. Any client can read, add or delete another user's history, and `user_id = 1` returns every user's history.  
- **Plain HTTP**: passwords, photos and GPS coordinates travel unencrypted.  
- **Exposed database**: `docker-compose.yml` publishes PostgreSQL on port 5432 to the host network.  
- **No abuse protection**: no rate limiting (login, Plant.id proxy), no request size limit, no timeout on the Plant.id call.  
- **Verbose errors**: raw exception messages, including database errors, are returned to the client.  
- **Development server**: the API runs on Flask's built-in server instead of a WSGI server such as gunicorn.  
- **Default admin account**: `init.sql` creates an `admin` user with a hardcoded demo password.  

**What is already handled**: every SQL query is parameterized (no SQL injection), passwords are hashed with scrypt, and secrets are loaded from a `.env` file that git ignores.  

A production version would add token-based authentication (JWT or signed sessions) with ownership checks on every query, create the admin account from an environment variable instead of a hardcoded password, run the API with gunicorn behind a TLS reverse proxy, keep the database on Docker's internal network only, and add rate limiting, input size limits and generic error responses.  

*This security review was carried out with the help of Claude (Anthropic), then checked against the code.*  

---