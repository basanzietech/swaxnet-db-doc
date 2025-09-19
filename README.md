# swaxnet-db-doc
Swaxnet Database Documentation 

# Swaxnet API Examples & Usage Guide

#### Create (POST)
```bash
# Add a new user using tableId=5
curl -X POST "https://www.api.swaxnet.xyz/api/data/secure.php?swax=5" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "username": "jane_smith",
    "email": "jane@example.com",
    "age": 30,
    "is_active": true,
    "created_at": "2024-01-15"
  }'
```

#### Read (GET)
```bash
# Get all users from tableId=5
curl -X GET "https://www.api.swaxnet.xyz/api/data/secure.php?swax=5" \
  -H "Authorization: Bearer YOUR_API_KEY"

# Get specific user by ID
curl -X GET "https://www.api.swaxnet.xyz/api/data/secure.php?swax=5&id=1" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

#### Update (PUT)
```bash
# Update user with ID 1 in tableId=5
curl -X PUT "https://www.api.swaxnet.xyz/api/data/secure.php?swax=5&id=1" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "username": "john_doe_updated",
    "age": 26,
    "is_active": false
  }'
```

#### Delete (DELETE)
```bash
# Delete user with ID 1 from table_id=5
curl -X DELETE "https://www.api.swaxnet.xyz/api/data/secure.php?swax=5&id=1" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### Error Response Format
```json
{
  "error": "Error message description"
}
```

### Common Error Examples

#### 401 - Unauthorized
```json
{
  "error": "API key required"
}
```

#### 404 - Table Not Found
```json
{
  "error": "Table not found"
}
```

#### 400 - Invalid Input
```json
{
  "error": "Table ID required"
}
```

#### 405 - Method Not Allowed
```json
{
  "error": "Method not allowed"
}
```

## Storage Operations


### Upload File
```bash
curl -X POST https://www.api.swaxnet.xyz/api/storage/upload.php \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "folder=profile_pictures" \
  -F "file=@/path/to/your/image.jpg"
```

## JavaScript Examples

### 🔒 Secure JavaScript Examples (RECOMMENDED)

```javascript
const API_KEY = 'your_api_key_here';
const BASE_URL = 'https://www.api.swaxnet.xyz/api';

// Get your tables first
async function getTables() {
  const response = await fetch(`${BASE_URL}/data/tables.php`, {
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    }
  });
  return await response.json();
}

// Create a new record (secure)
async function createUser(userData) {
  const response = await fetch(`${BASE_URL}/data/secure.php?swax=5`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${API_KEY}`
    },
    body: JSON.stringify(userData)
  });
  return await response.json();
}

// Get all users (secure)
async function getUsers() {
  const response = await fetch(`${BASE_URL}/data/secure.php?swax=5`, {
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    }
  });
  return await response.json();
}

// Update user (secure)
async function updateUser(userId, updateData) {
  const response = await fetch(`${BASE_URL}/data/secure.php?swax=5&id=${userId}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${API_KEY}`
    },
    body: JSON.stringify(updateData)
  });
  return await response.json();
}

// Delete user (secure)
async function deleteUser(userId) {
  const response = await fetch(`${BASE_URL}/data/secure.php?swax=5&id=${userId}`, {
    method: 'DELETE',
    headers: {
      'Authorization': `Bearer ${API_KEY}`
    }
  });
  return await response.json();
}

// Usage examples
getTables().then(tables => {
  console.log('Your tables:', tables);
});

createUser({
  username: 'alice',
  email: 'alice@example.com',
  age: 28
}).then(result => console.log(result));

getUsers().then(users => console.log(users));
```


### Using Axios (Secure Method)
```javascript
const axios = require('axios');

const API_KEY = 'your_api_key_here';
const BASE_URL = 'https://www.api.swaxnet.xyz/api';

const api = axios.create({
  baseURL: BASE_URL,
  headers: {
    'Authorization': `Bearer ${API_KEY}`,
    'Content-Type': 'application/json'
  }
});

// Get your tables first
async function getTables() {
  try {
    const response = await api.get('/data/tables.php');
    return response.data;
  } catch (error) {
    console.error('Error getting tables:', error.response.data);
  }
}

// Create table
async function createTable(tableName) {
  try {
    const response = await api.post('/tables/create.php', {
      table_name: tableName
    });
    return response.data;
  } catch (error) {
    console.error('Error creating table:', error.response.data);
  }
}

// Secure CRUD operations
const tableId = 5; // Get this from getTables()

// Create
const newProduct = await api.post(`/data/secure.php?swax=${tableId}`, {
  name: 'iPhone 15',
  price: 999.99,
  category: 'electronics'
});

// Read
const products = await api.get(`/data/secure.php?swax=${tableId}`);
const product = await api.get(`/data/secure.php?swax=${tableId}&id=1`);

// Update
const updatedProduct = await api.put(`/data/secure.php?swax=${tableId}&id=1`, {
  price: 899.99,
  in_stock: false
});

// Delete
await api.delete(`/data/secure.php?swax=${tableId}&id=1`);
```

## Python Examples

### Using requests library (Secure Method)
```python
import requests
import json

API_KEY = 'your_api_key_here'
BASE_URL = 'https://www.api.swaxnet.xyz/api'

headers = {
    'Authorization': f'Bearer {API_KEY}',
    'Content-Type': 'application/json'
}

# Get your tables first
def get_tables():
    response = requests.get(f'{BASE_URL}/data/tables.php', headers=headers)
    return response.json()

# Secure CRUD operations
table_id = 5  # Get this from get_tables()

# Create
def create_user(user_data):
    response = requests.post(
        f'{BASE_URL}/data/secure.php?swax={table_id}',
        headers=headers,
        json=user_data
    )
    return response.json()

# Read
def get_users():
    response = requests.get(f'{BASE_URL}/data/secure.php?swax={table_id}', headers=headers)
    return response.json()

def get_user(user_id):
    response = requests.get(f'{BASE_URL}/data/secure.php?swax={table_id}&id={user_id}', headers=headers)
    return response.json()

# Update
def update_user(user_id, update_data):
    response = requests.put(
        f'{BASE_URL}/data/secure.php?swax={table_id}&id={user_id}',
        headers=headers,
        json=update_data
    )
    return response.json()

# Delete
def delete_user(user_id):
    response = requests.delete(f'{BASE_URL}/data/secure.php?swax={table_id}&id={user_id}', headers=headers)
    return response.json()

# Usage examples
tables = get_tables()
print('Your tables:', tables)

new_user = create_user({
    'username': 'alice',
    'email': 'alice@example.com',
    'age': 28
})
print('Created user:', new_user)

users = get_users()
print('All users:', users)
```

## 🗄️ Table CRUD (Create, Read, Update, Delete)

### Create (Insert Data)
```bash
POST /api/data/secure.php?swax=TABLE_ID
Headers: Authorization: Bearer YOUR_API_KEY
Content-Type: application/json

Body:
{
  "username": "john_doe",
  "email": "john@example.com"
}
```
**Success:**
```json
{
  "success": true,
  "message": "Record inserted successfully"
}
```
**Error:**
```json
{
  "error": "Table not found"
}
```

### Read (Get Data)
```bash
GET /api/data/secure.php?swax=TABLE_ID
Headers: Authorization: Bearer YOUR_API_KEY
```
**Success:**
```json
{
  "success": true,
  "data": [ { "id": 1, "username": "john_doe" } ]
}
```

### Update
```bash
PUT /api/data/secure.php?swax=TABLE_ID&id=RECORD_ID
Headers: Authorization: Bearer YOUR_API_KEY
Content-Type: application/json

Body:
{
  "username": "john_updated"
}
```
**Success:**
```json
{
  "success": true,
  "message": "Record updated successfully"
}
```

### Delete
```bash
DELETE /api/data/secure.php?swax=TABLE_ID&id=RECORD_ID
Headers: Authorization: Bearer YOUR_API_KEY
```
**Success:**
```json
{
  "success": true,
  "message": "Record deleted successfully"
}
```

## 📤 Table Export & Backup


## 📁 File Storage CRUD (Upload, List, Download, Delete)

### Upload File
```bash
POST /api/storage/upload.php
Headers: Authorization: Bearer YOUR_API_KEY
Content-Type: multipart/form-data

Form Data:
- folder: FOLDER_NAME
- file: (select file)
```
**Success:**
```json
{
  "success": true,
  "message": "File uploaded successfully",
  "filename": "randomname.jpg"
}
```
**Error:**
```json
{
  "error": "File extension not allowed"
}
```

### List Folders

## 🛑 Error & Success Messages
- All endpoints return either `{ "success": true, ... }` or `{ "error": "..." }`
- Common errors: `Table not found`, `Invalid API key`, `File extension not allowed`, `Storage limit exceeded`, `Folder not found`, `Record not found`


## 📞 Support

For security questions or issues:
- WhatsApp: +255657779003
- Email: support@swaxnet.xyz
- Documentation: See `SECURE_API_GUIDE.md` 
