
```
## 📥 Data Insertion

The following commands insert sample data into the tables:

```sql
INSERT INTO client (nom, telephone, adresse) VALUES
('Ahmed Saidi', '0612345678', 'Casablanca, Maroc'),
('Fatima El Amri', '0678901234',  'Rabat, Maroc');

select * from client;

INSERT INTO voiture (marque, modele, annee,immatriculation) VALUES
('Toyota', 'Corolla', '2020','1234ABC'),
('Renault', 'clio',  '2021','5678XYZ');

select * from voiture;

select * from location;
INSERT INTO location (id_client, id_voiture, date_debut, date_fin, prix_total) VALUES
(1, 1, '2024-01-01', '2024-01-10','30'),
(2, 2, '2024-02-01', '2024-02-10','40');

```

---

---
# Database Documentation

## Welcome to the Project Documentation

This documentation outlines the steps to create, manage, and query a relational database for a car rental system. The database consists of three main tables: `client`, `voiture`, and `location`, which are interconnected to manage clients, vehicles, and rental contracts efficiently.

---

## ☎️ Project Overview

The database contains the following tables:

1. **Client Table**: Stores client information, such as their name, phone number, and address.
2. **Voiture Table**: Stores vehicle information, including its ID, brand, model, year, and immatriculation.
3. **Location Table**: Tracks rental transactions, linking clients to vehicles and recording rental details like start date, end date, and total price.

---

## 📁 Tables Creation

The SQL commands below define the database schema and establish relationships between the tables:

### 1. Create the `client` Table
```sql
use car_rental_system;
CREATE TABLE client(
    id_client INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    prenom VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telephone VARCHAR(15) NOT NULL,
    adresse TEXT NOT NULL,
    permis_conduire VARCHAR(20) UNIQUE NOT NULL,
    date_inscription DATE NOT NULL
);


```

### 2. Create the `voiture` Table
```sql
CREATE TABLE voiture (
    id_voiture INT PRIMARY KEY AUTO_INCREMENT,
    marque VARCHAR(50) NOT NULL,
    modele VARCHAR(50) NOT NULL,
    annee YEAR NOT NULL,
    immatriculation VARCHAR(20) UNIQUE NOT NULL,
    kilometrage INT NOT NULL,
    prix_jour DECIMAL(10,2) NOT NULL,
    disponible BOOLEAN DEFAULT true,
    categorie ENUM('economique', 'berline', 'luxe', 'utilitaire') NOT NULL
);
```

### 3. Create the `location` Table
```sql
CREATE TABLE location (
    id_location INT PRIMARY KEY AUTO_INCREMENT,
    id_client int,
    id_voiture int,
    date_debut DATE,
    date_fin DATE,
    prix_total DECIMAL(10,2),
    FOREIGN KEY (id_client) REFERENCES client (id_client),
    FOREIGN KEY (id_voiture) REFERENCES voiture (id_voiture)
);
```

---

## 📥 Data Insertion

Here are sample `INSERT` statements to populate the tables with data:

### Insert Data into `client`
```sql
INSERT INTO client (nom, telephone, adresse) VALUES
('Ali Benomar', '0612345678', 'Casablanca, Maroc'),
('Salma Khadiri', '0678901234', 'Rabat, Maroc');
```

### Insert Data into `voiture`
```sql
INSERT INTO voiture (marque, modele, annee, immatriculation) VALUES
('Toyota', 'Corolla', 2020, '1234ABC'),
('Renault', 'Clio', 2021, '5678XYZ');
```

### Insert Data into `location`
```sql
INSERT INTO location (id_client, id_voiture, date_debut, date_fin, prix_total) VALUES
(1, 1, '2024-01-01', '2024-01-10', 1000.00),
(2, 2, '2024-02-01', '2024-02-05', 500.00);
```

---

## 🔍 Queries and Operations

### 1. Display All Rental Transactions
```sql
SELECT
    location.id_location,
    client.nom AS client_name,
    voiture.marque AS car_brand,
    voiture.modele AS car_model,
    location.date_debut,
    location.date_fin,
    location.prix_total
FROM location
INNER JOIN client ON location.id_client = client.id_client
INNER JOIN voiture ON location.id_voiture = voiture.id_voiture;
```

### 2. Find Rentals Over a Certain Price
```sql
SELECT *
FROM location
WHERE prix_total > 800.00;
```

### 3. Add a New Rental
```sql
INSERT INTO location (id_client, id_voiture, date_debut, date_fin, prix_total)
VALUES (3, 1, '2024-03-01', '2024-03-07', 700.00);
```

### 4. Update Rental Price
```sql
UPDATE location
SET prix_total = 1200.00
WHERE id_location = 1;
```

### 5. Delete Old Rentals
```sql
DELETE FROM location
WHERE date_fin < '2024-02-01';
```

---

## 🔧 Tools and Technologies

- **Database**: MySQL
- **SQL Environment**: MySQL Workbench, phpMyAdmin, or other SQL clients

---

## 🖌️ Notes

1. The `id_voiture` column in the `location` table references the `id_voiture` column in the `voiture` table.
2. All data operations should follow the integrity constraints defined by the foreign keys.
3. Adjust the datatype of columns based on specific project requirements.

---

This documentation provides all essential details for setting up and managing the database. Happy coding!



