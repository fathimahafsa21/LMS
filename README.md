# Library Member Management System


This project is a Java application designed to manage member information for a library.


## Classes

The project consists of the following classes:

* **Crud:** Handles database queries, including inserts, updates, deletes, and selects.
* **DbConnection:** Establishes and manages the database connection.
* **MemberManagementForm:** Provides the graphical user interface for interacting with member data.

## Functionality

The application supports the following functionalities:

* **Adding new members:**
* **Searching for members by ID:**
* **Viewing member details in a table:**
* **Updating member information:**
* **Deleting members:**

## My Work

 ### NAME: M.H.F.HAFSA
 ### REG.NO: KEG/IT/2021/F/0074

In our library member management system, I've developed the 'member insertion' functionality and few button actions. This feature enables users to seamlessly add new members to the system, thereby enhancing its functionality and usability.

### Description of Functions

It is like clear/reset button. When press it. It clears any text or data you've entered and it allows you to type in a special box again and it changes the label on another button to say "Save" again.


When press the "Save" button:

* It checks if all required fields are filled.
* If they are, it saves the member's information into a database.
* If successful, it tells the member is saved and clears the form for the next entry.
* If there's a problem, it lets know and logs the issue for someone to look into later.


## Code Snippets

***Here is some functions and events which i contribute to the group***
```java


    private void btnClearActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnClearActionPerformed
        clearForm();
        txtMemberId.setEditable(true);
        btnSave.setText("Save");
    }

    private void btnSaveActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnSaveActionPerformed
        if(txtMemberId.getText().equals("") || txtName.getText().equals("") || txtEmail.getText().equals("") || txtPhoneNumber.getText().equals("") || txtAddress.getText().equals("")){
            JOptionPane.showMessageDialog(this, "fill all fiels!");
            return;
        }
        try {
            Crud.execute("INSERT INTO member VALUES(?,?,?,?,?)", txtMemberId.getText(), txtName.getText(), txtEmail.getText(), txtPhoneNumber.getText(), txtAddress.getText());
            JOptionPane.showMessageDialog(this, "Member saved successfully!");
            clearForm();
            loadMembersIntoTable();
        } catch (SQLException | ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(this, "Error saving member. Please check your input and try again.", "Error", JOptionPane.ERROR_MESSAGE);
            Logger.getLogger(MemberManagementForm.class.getName()).log(Level.SEVERE, null, ex);
        }
    }

