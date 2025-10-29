import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

class ParcelTrackingSystem extends Frame implements ActionListener {
    // Components for Login Screen
    TextField usernameField, passwordField;
    Button loginButton;

    // Components for Dashboard
    Button trackParcelButton, updateParcelButton;

    // Parcel data structure
    ArrayList<Parcel> parcels = new ArrayList<>();

    // Constructor
    public ParcelTrackingSystem() {
        // Pre-fill some parcel data with item names
        parcels.add(new Parcel("P001", "Alice", "Bob", "In Transit", "New York", "Los Angeles", "Electronics"));
        parcels.add(new Parcel("P002", "Charlie", "Dave", "Delivered", "Chicago", "Houston", "Clothing"));
        parcels.add(new Parcel("P003", "Eve", "Frank", "Pending", "San Francisco", "Miami", "Books"));
        parcels.add(new Parcel("P004", "Grace", "Hank", "In Transit", "London", "Berlin", "Furniture"));
        parcels.add(new Parcel("P005", "Ivy", "Jack", "Delivered", "Tokyo", "Seoul", "Toys"));
        parcels.add(new Parcel("P006", "John", "Kate", "In Transit", "Toronto", "Vancouver", "Gadgets"));
        parcels.add(new Parcel("P007", "Liam", "Mia", "Delivered", "Paris", "Madrid", "Accessories"));
        parcels.add(new Parcel("P008", "Nina", "Oscar", "Pending", "Rome", "Athens", "Sports Gear"));
        parcels.add(new Parcel("P009", "Paul", "Quinn", "In Transit", "Bangkok", "Kuala Lumpur", "Stationery"));
        parcels.add(new Parcel("P010", "Rachel", "Steve", "Delivered", "Mumbai", "Delhi", "Home Decor"));
        parcels.add(new Parcel("P011", "Sophia", "Tom", "Pending", "Dubai", "Abu Dhabi", "Cosmetics"));
        parcels.add(new Parcel("P012", "Uma", "Victor", "In Transit", "Sydney", "Brisbane", "Books"));
        parcels.add(new Parcel("P013", "Walter", "Xena", "Delivered", "Cape Town", "Johannesburg", "Food Items"));
        parcels.add(new Parcel("P014", "Yara", "Zane", "Pending", "Shanghai", "Beijing", "Toys"));
        parcels.add(new Parcel("P015", "Aaron", "Bella", "In Transit", "Los Angeles", "San Diego", "Electronics"));


        // Set up the login screen
        setTitle("Parcel Tracking System - Login");
        setSize(500, 300);
        setLayout(null);
        setBackground(Color.LIGHT_GRAY);

        Label userLabel = new Label("Username :");
        userLabel.setBounds(50, 80, 100, 30);
        add(userLabel);

        usernameField = new TextField();
        usernameField.setBounds(160, 80, 200, 30);
        add(usernameField);

        Label passLabel = new Label("Password :");
        passLabel.setBounds(50, 130, 100, 30);
        add(passLabel);

        passwordField = new TextField();
        passwordField.setBounds(160, 130, 200, 30);
        passwordField.setEchoChar('*');
        add(passwordField);

        loginButton = new Button("Login");
        loginButton.setBounds(200, 180, 100, 30);
        loginButton.setBackground(Color.BLUE);
        loginButton.setForeground(Color.WHITE);
        loginButton.addActionListener(this);
        add(loginButton);

        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                dispose();
            }
        });
    }

    // Dashboard
    public void showDashboard() {
        removeAll();
        setTitle("Parcel Tracking System - Dashboard");
        setSize(600, 400);
        setBackground(Color.LIGHT_GRAY);

        trackParcelButton = new Button("Track Parcel");
        trackParcelButton.setBounds(200, 100, 200, 50);
        trackParcelButton.setBackground(Color.CYAN);
        trackParcelButton.addActionListener(this);
        add(trackParcelButton);

        updateParcelButton = new Button("Update Parcel");
        updateParcelButton.setBounds(200, 200, 200, 50);
        updateParcelButton.setBackground(Color.GREEN);
        updateParcelButton.addActionListener(this);
        add(updateParcelButton);

        repaint();
        validate();
    }

    // Tracking
    public void showTracking() {
        removeAll();
        setTitle("Track Parcel");
        setSize(600, 500);
        setBackground(Color.CYAN);

        Label trackingLabel = new Label("Parcel Tracking");
        trackingLabel.setBounds(50, 50, 500, 30);
        trackingLabel.setFont(new Font("Arial", Font.BOLD, 20));
        trackingLabel.setForeground(Color.BLACK);
        add(trackingLabel);

        // Ask for Parcel ID
        Label parcelIDLabel = new Label("Enter Parcel ID to Track :");
        parcelIDLabel.setBounds(50, 100, 200, 30);
        add(parcelIDLabel);

        TextField parcelIDField = new TextField();
        parcelIDField.setBounds(250, 100, 200, 30);
        add(parcelIDField);

        Button trackButton = new Button("Track");
        trackButton.setBounds(460, 100, 100, 30);
        trackButton.addActionListener(e -> trackParcel(parcelIDField.getText()));
        add(trackButton);

        repaint();
        validate();
    }

    // Track Parcel by ID
    private void trackParcel(String parcelID) {
        for (Parcel parcel : parcels) {
            if (parcel.getId().equalsIgnoreCase(parcelID)) {
                showParcelDetails(parcel);
                return;
            }
        }
        showError("Parcel not found! Please check the ID.");
    }

    // Show Parcel Details
    private void showParcelDetails(Parcel parcel) {
        removeAll();
        setTitle("Parcel Details");
        setSize(600, 400);
        setBackground(Color.LIGHT_GRAY);

        Label parcelInfoLabel = new Label("Parcel ID            :   " + parcel.getId());
        parcelInfoLabel.setBounds(100, 50, 500, 30);
        add(parcelInfoLabel);

        Label itemNameLabel = new Label("Item                    :   " + parcel.getItemName());
        itemNameLabel.setBounds(100, 100, 500, 30);
        add(itemNameLabel);

        Label senderLabel = new Label("Sender               :   " + parcel.getSender());
        senderLabel.setBounds(100, 150, 500, 30);
        add(senderLabel);

        Label recipientLabel = new Label("Recipient            :   " + parcel.getRecipient());
        recipientLabel.setBounds(100, 200, 500, 30);
        add(recipientLabel);

        Label startLocationLabel = new Label("Start Location     :   " + parcel.getStartLocation());
        startLocationLabel.setBounds(100, 250, 500, 30);
        add(startLocationLabel);

        Label endLocationLabel = new Label("End Location      :   " + parcel.getEndLocation());
        endLocationLabel.setBounds(100, 300, 500, 30); 
        add(endLocationLabel);

        Label statusLabel = new Label("Current Status   :   " + parcel.getStatus());
        statusLabel.setBounds(100, 350, 500, 30);
        add(statusLabel);

        repaint();
        validate();
    }

    // Update Parcel Status
    private void showUpdateParcelForm() {
        removeAll();
        setTitle("Update Parcel Status");
        setSize(600, 400);
        setBackground(Color.LIGHT_GRAY);

        Label parcelIDLabel = new Label("Enter Parcel ID to Update :");
        parcelIDLabel.setBounds(50, 50, 200, 30);
        add(parcelIDLabel);

        TextField parcelIDField = new TextField();
        parcelIDField.setBounds(250, 50, 200, 30);
        add(parcelIDField);

        Button findParcelButton = new Button("Find Parcel");
        findParcelButton.setBounds(460, 50, 100, 30);
        findParcelButton.addActionListener(e -> updateParcel(parcelIDField.getText()));
        add(findParcelButton);

        repaint();
        validate();
    }

    // Find and Update Parcel
    private void updateParcel(String parcelID) {
        for (Parcel parcel : parcels) {
            if (parcel.getId().equalsIgnoreCase(parcelID)) {
                // Show the update form with current data
                showParcelUpdateForm(parcel);
                return;
            }
        }
        showError("Parcel not found! Please check the ID.");
    }

    // Show Update Parcel Form
    private void showParcelUpdateForm(Parcel parcel) {
        removeAll();
        setTitle("Update Parcel Details");
        setSize(600, 400);
        setBackground(Color.LIGHT_GRAY);

        Label parcelIDLabel = new Label("Parcel ID: " + parcel.getId());
        parcelIDLabel.setBounds(50, 50, 200, 30);
        add(parcelIDLabel);

        Label itemNameLabel = new Label("Item: " + parcel.getItemName());
        itemNameLabel.setBounds(50, 100, 500, 30);
        add(itemNameLabel);

        Label statusLabel = new Label("Current Status: " + parcel.getStatus());
        statusLabel.setBounds(50, 150, 200, 30);
        add(statusLabel);

        Label newStatusLabel = new Label("New Status:");
        newStatusLabel.setBounds(50, 200, 200, 30);
        add(newStatusLabel);

        TextField newStatusField = new TextField(parcel.getStatus());
        newStatusField.setBounds(250, 200, 200, 30);
        add(newStatusField);

        Button saveButton = new Button("Update Status");
        saveButton.setBounds(200, 250, 150, 30);
        saveButton.addActionListener(e -> updateParcelStatus(parcel, newStatusField.getText()));
        add(saveButton);

        repaint();
        validate();
    }

    // Update Parcel Status in the List
    private void updateParcelStatus(Parcel parcel, String newStatus) {
        parcel.setStatus(newStatus);
        showParcelDetails(parcel);
    }

    // Show error dialog
    private void showError(String message) {
        Dialog errorDialog = new Dialog(this, "Error", true);
        errorDialog.setLayout(new FlowLayout());
        errorDialog.add(new Label(message));
        Button okButton = new Button("OK");
        okButton.addActionListener(ev -> errorDialog.setVisible(false));
        errorDialog.add(okButton);
        errorDialog.setSize(300, 100);
        errorDialog.setVisible(true);
    }

    // Handle actions
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == loginButton) {
            if (usernameField.getText().equals("admin") && passwordField.getText().equals("password")) {
                showDashboard();
            } else {
                showError("Invalid credentials! Try again.");
            }
        } else if (e.getSource() == trackParcelButton) {
            showTracking();
        } else if (e.getSource() == updateParcelButton) {
            showUpdateParcelForm();
        }
    }

    // Parcel class
    static class Parcel {
        private String id;
        private String sender;
        private String recipient;
        private String status;
        private String startLocation;
        private String endLocation;
        private String itemName; // New field for the item being tracked

        Parcel(String id, String sender, String recipient, String status, String startLocation, String endLocation, String itemName) {
            this.id = id;
            this.sender = sender;
            this.recipient = recipient;
            this.status = status;
            this.startLocation = startLocation;
            this.endLocation = endLocation;
            this.itemName = itemName;
        }

        public String getId() {
            return id;
        }

        public String getSender() {
            return sender;
        }

        public String getRecipient() {
            return recipient;
        }

        public String getStatus() {
            return status;
        }

        public String getStartLocation() {
            return startLocation;
        }

        public String getEndLocation() {
            return endLocation;
        }

        public String getItemName() {
            return itemName;
        }

        public void setStatus(String status) {
            this.status = status;
        }
    }

    // Main method
    public static void main(String[] args) {
        ParcelTrackingSystem system = new ParcelTrackingSystem();
        system.setVisible(true);
    }
}

