# URL Shortener in Go

This project is a simple URL shortener written in Go. It allows users to shorten long URLs and then retrieve the original URLs using the shortened versions. The shortened URLs are stored in an in-memory database.

## Features

- **Shorten URLs**: Converts long URLs into shorter, 8-character versions using MD5 hashing.
- **Redirect**: Redirects users from a shortened URL to the original URL.
- **In-Memory Database**: Stores the mapping between shortened and original URLs in a map.

## How It Works

1. **URL Shortening**:
   - Users send a POST request to `/shorten` with a JSON body containing the original URL.
   - The server generates a shortened URL using the first 8 characters of an MD5 hash of the original URL.
   - The shortened URL is stored in an in-memory map with the original URL.
   - The server returns the shortened URL in the response.

2. **Redirecting**:
   - Users can access the original URL by visiting `/redirect/{shortURL}`.
   - The server looks up the original URL using the `shortURL` from the in-memory map.
   - If found, the server redirects the user to the original URL.

## Endpoints

- **GET `/`**: Returns a simple "Hello, World!" message.
- **POST `/shorten`**: Accepts a JSON body with a URL to shorten. Returns the shortened URL.
- **GET `/redirect/{shortURL}`**: Redirects to the original URL associated with the `shortURL`.

## Example Usage

### Shorten a URL

To shorten a URL, send a POST request to `/shorten` with the following JSON body:

```json
{
    "url": "https://www.example.com"
}
```

Response:

```json
{
    "short_url": "d41d8cd9"
}
```

### Redirect to Original URL

Visit `/redirect/d41d8cd9` in your browser, and you will be redirected to `https://www.example.com`.

## Running the Project

### Prerequisites

- [Go](https://golang.org/doc/install) (version 1.18 or later)

### Steps

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/your-username/url-shortener-go.git
   cd url-shortener-go
   ```

2. **Run the Application**:

   ```bash
   go run main.go
   ```

3. **Access the Server**:

   - The server will start on `http://localhost:3000`.
   - Use tools like `curl`, Postman, or your browser to interact with the endpoints.

## Future Improvements

- Add persistent storage (e.g., a database) instead of using an in-memory map.
- Implement expiration for shortened URLs.
- Add unit tests to cover all functionality.

## Contributing

Feel free to fork this repository and submit pull requests. Any contributions are welcome!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
