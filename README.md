# Fuming Database

[![npm version](https://img.shields.io/npm/v/fuming.svg)](https://www.npmjs.com/package/fuming)
[![TypeScript](https://img.shields.io/badge/TypeScript-Ready-blue.svg)](https://www.typescriptlang.org/)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

**Fuming** is a lightweight and efficient database management system built with TypeScript. It simplifies database operations with type safety, robust query handling, and seamless integration into any modern web application.

## Features

- 🚀 **Lightweight & Fast**: Minimal overhead with efficient file-based storage
- 📘 **TypeScript Support**: Full type safety and excellent IDE integration
- 🔄 **CRUD Operations**: Complete set of Create, Read, Update, and Delete operations
- 🛠️ **Easy Setup**: Simple installation and minimal configuration
- 📁 **Collection-based**: Organize your data in collections, similar to MongoDB
- 🆔 **Automatic ID Generation**: Built-in unique ID generation for documents

## Installation

```bash
npm install fuming
```

## Quick Start

```typescript
import { connect, collection } from 'fuming';

// Connect to database
const db = await connect('mydb');

// Create a collection
collection.create('users');

// Insert data
await collection.insert('users', {
  name: 'John Doe',
  email: 'john@example.com',
  age: 30
});

// Find all documents
const users = collection.find('users');
console.log(users);
```

## API Reference

### Connection

#### `connect(dbname: string): Promise<string[]>`
Connects to a database. Creates the database directory if it doesn't exist.

```typescript
const collections = await connect('mydb');
// Returns array of existing collection names
```

### Collections

#### `collection.create(collection: string)`
Creates a new collection.

```typescript
collection.create('users');
```

#### `collection.find(collection: string)`
Retrieves all documents from a collection.

```typescript
const users = collection.find('users');
```

#### `collection.insert(collection: string, newData: any)`
Inserts a new document into a collection. Automatically generates a unique `_id`.

```typescript
await collection.insert('users', {
  name: 'Jane Doe',
  email: 'jane@example.com'
});
```

#### `collection.update(collection: string, { key, value }, newData)`
Updates a document in a collection based on a key-value pair.

```typescript
await collection.update('users', 
  { key: 'email', value: 'john@example.com' },
  {
    name: 'John Smith',
    email: 'john@example.com'
  }
);
```

#### `collection.remove(collection: string, { key, value })`
Removes a document from a collection based on a key-value pair.

```typescript
await collection.remove('users', {
  key: 'email',
  value: 'john@example.com'
});
```

#### `collection.destroy(collection: string)`
Deletes an entire collection.

```typescript
await collection.destroy('users');
```

## Data Structure

Each document in a collection automatically receives a unique `_id` field when inserted:

```typescript
{
  "_id": "lqr1k3j4x9ab2m5n",
  "name": "John Doe",
  "email": "john@example.com"
}
```

## Example Usage

### Creating a User Management System

```typescript
import { connect, collection } from 'fuming';

async function initializeDatabase() {
  // Connect to database
  await connect('userdb');
  
  // Create users collection
  collection.create('users');
}

async function addUser(userData: any) {
  return await collection.insert('users', userData);
}

async function updateUserEmail(oldEmail: string, newData: any) {
  return await collection.update('users', 
    { key: 'email', value: oldEmail },
    newData
  );
}

async function deleteUser(email: string) {
  return await collection.remove('users', {
    key: 'email',
    value: email
  });
}

// Usage
initializeDatabase()
  .then(() => addUser({
    name: 'John Doe',
    email: 'john@example.com',
    role: 'admin'
  }))
  .catch(console.error);
```

## Notes

- All collection operations are file-based and synchronous
- Data is stored in JSON format
- Each database is a directory containing JSON files for each collection
- The database name is stored in the environment variables
- Collection names map directly to JSON files

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. By contributing to this project, you agree to abide by its terms.

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

### GNU GPL v3
Fuming is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.