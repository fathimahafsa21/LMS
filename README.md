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

In our library member management system, I've developed the 'book insertion' functionality and few button actions releted to book insertion. This feature enables users to seamlessly add new members to the system, thereby enhancing its functionality and usability. I have uploaded my work, including the code and functionalities, via the link below. Thank you.



## Code Snippets

***Here is some shorted class***
```java
private void btnClearActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnClearActionPerformed
        clearForm();
        txtMemberId.setEditable(true);
        btnSave.setText("Save");
    }//GEN-LAST:event_btnClearActionPerformed

    private void clearForm() {
        txtMemberId.setText("");
        txtName.setText("");
        txtPhoneNumber.setText("");
        txtEmail.setText("");
        txtAddress.setText("");
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
    }//GEN-LAST:event_btnSaveActionPerformed

    private void btnSearchActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnSearchActionPerformed
        try {
            ResultSet resultSet = Crud.execute("SELECT * FROM member WHERE member_id=?", txtId.getText());
            if (resultSet.next()) {
                txtMemberId.setText(resultSet.getString(1));
                txtName.setText(resultSet.getString(2));
                txtEmail.setText(resultSet.getString(3));
                txtPhoneNumber.setText(resultSet.getString(4));
                txtAddress.setText(resultSet.getString(5));

                JOptionPane.showMessageDialog(this, "Member found!");
                txtId.setText("");
                txtMemberId.setEditable(false);

                for (ActionListener al : btnSave.getActionListeners()) {
                    btnSave.removeActionListener(al);
                }

                btnSave.setText("Update");
                btnSave.addActionListener(new ActionListener() {
                    @Override
                    public void actionPerformed(ActionEvent e) {
                        try {
                            update();
                            txtMemberId.setEditable(true);
                        } catch (SQLException | ClassNotFoundException ex) {
                            JOptionPane.showMessageDialog(MemberManagementForm.this, "Error updating member. Please try again.", "Error", JOptionPane.ERROR_MESSAGE);
                            Logger.getLogger(MemberManagementForm.class.getName()).log(Level.SEVERE, null, ex);
                        }
                    }
                });

            } else {
                JOptionPane.showMessageDialog(this, "No member found with the given ID.", "Not Found", JOptionPane.INFORMATION_MESSAGE);
            }
        } catch (SQLException | ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(this, "Error searching for member. Please try again.", "Error", JOptionPane.ERROR_MESSAGE);
            Logger.getLogger(MemberManagementForm.class.getName()).log(Level.SEVERE, null, ex);
        }
    }//GEN-LAST:event_btnSearchActionPerformed

    private void update() throws SQLException, ClassNotFoundException {
        Crud.execute("UPDATE member SET name = ?, email = ?, phone_number = ?, address = ? WHERE member_id = ?",
                txtName.getText(), txtEmail.getText(), txtPhoneNumber.getText(), txtAddress.getText(), txtMemberId.getText());
        JOptionPane.showMessageDialog(this, "Member Updated successfully!");
        btnSave.setText("Save");
        clearForm();
        loadMembersIntoTable();
    }

    private void btnDeleteActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnDeleteActionPerformed
        try {
            Crud.execute("DELETE FROM member WHERE member_id=?", txtId.getText());
            JOptionPane.showMessageDialog(this, "Member deleted successfully!");
            txtId.setText("");
            clearForm();
            loadMembersIntoTable();
        } catch (SQLException | ClassNotFoundException ex) {
            JOptionPane.showMessageDialog(this, "Error deleting member. Please check the member ID and try again.", "Error", JOptionPane.ERROR_MESSAGE);
            Logger.getLogger(MemberManagementForm.class.getName()).log(Level.SEVERE, null, ex);
        }
    }//GEN-LAST:event_btnDeleteActionPerformed

    private void loadMembersIntoTable() {
        try {
            ResultSet resultSet = Crud.execute("SELECT * FROM member");

            DefaultTableModel model = new DefaultTableModel();
            model.addColumn("Member Id");
            model.addColumn("Name");
            model.addColumn("Email");
            model.addColumn("Phone Number");
            model.addColumn("Address");

            while (resultSet.next()) {
                model.addRow(new Object[]{resultSet.getString(1), resultSet.getString(2), resultSet.getString(3), resultSet.getString(4), resultSet.getString(5)});
            }

            tblMember.setModel(model);
        } catch (SQLException | ClassNotFoundException ex) {
            Logger.getLogger(MemberManagementForm.class.getName()).log(Level.SEVERE, null, ex);
        }
    }

