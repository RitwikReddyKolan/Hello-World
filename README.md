# Hello-World
My Repository On Git-Hub


<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
    <head>
        <title>Bootstrap Example</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
        src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
        src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
    </head>
    <body>
        <div class="container">
            <h2>STUDENT DETAILS FORM</h2>
            <form id="studentForm" method="post">
                <div class="form-group">
                    <span><label for="StudentRoll-No">Student Roll-No:</label> <label id="studentRoll-NoMsg">
                        </label></span>
                    <input type="text" class="form-control" name="studentRoll-No" id="studentRoll-No"
                           placeholder="Enter Student Roll-No" required>
                </div>
                <div class="form-group">
                    <label for="studentName">Student Name:</label>
                    <input type="text" class="form-control" id="studentName"
                           placeholder="Enter Student Name" name="studentName">
                </div>
                <div class="form-group">
                    <label for="studentClass">Class:</label>
                    <input type="text" class="form-control" id="studentClass"
                           placeholder="Enter Student Class" name="studentClass">
                </div>
                <div class="form-group">
                    <label for="Birth-Date">Birth-Date:</label>
                    <input type="text" class="form-control" id="Birth-Date"
                           placeholder="Enter Student Birth-Date" name="Birth-Date">
                </div>
                <div class="form-group">
                    <label for="Address">Address:</label>
                    <input type="text" class="form-control" id="Address"
                           placeholder="Enter Student Address" name="Address">
                </div>
                <div class="form-group">
                    <label for="EnrollmentDate">EnrollmentDate:</label>
                    <input type="text" class="form-control" id="EnrollmentDate"
                           placeholder="Enter Student EnrollmentDate" name="EnrollmentDate">
                </div>
                <input type="button" class="btn btn-primary" id="studentSave" value="Save"
                       onclick="saveStudent();">
                <input type="button" class="btn btn-primary" id="studentUpdate" value="Update"
                       onclick="updateStudent();">
                <input type="button" class="btn btn-primary" id="studentReset" value="Reset"
                       onclick="resetStudent();">
            </form>
        </div>
        <script>
            $("#studentRollno").focus();
            function validateAndGetFormData() {
                var studentRollnoVar = $("#studentRollno").val();
                if (studentRollnoVar === "") {
                    alert("Student Rollno Required Value");
                    $("#studentRollno").focus();
                    return "";
                }
                var studentNameVar = $("#studentName").val();
                if (studentNameVar === "") {
                    alert("Student Name is Required Value");
                    $("#studentName").focus();
                    return "";
                }
                var studentClassVar = $("#studentClass").val();
                if (studentClassVar === "") {
                    alert("Student Class is Required Value");
                    $("#studentClass").focus();
                    return "";
                }
                var BirthDateVar = $("#BirthDate").val();
                if (BirthDateVar === "") {
                    alert("Student BirthDate is Required Value");
                    $("#BirthDate").focus();
                    return "";
                }
                var AddressVar = $("#Address").val();
                if (AddressVar === "") {
                    alert("Student Address is Required Value");
                    $("#Address").focus();
                    return "";
                }
                var EnrollmentDateVar = $("#EnrollmentDate").val();
                if (EnrollmentDateVar === "") {
                    alert("Student EnrollmentDate is Required Value");
                    $("#EnrollmentDate").focus();
                    return "";
                }
                var jsonStrObj = {
                    studentRollno: studentRollnoVar,
                    studentName: studentNameVar,
                    studentClass: studentClassVar,
                    BirthDate: BirthDateVar,
                    Address: AddressVar,
                    EnrollmentDate: EnrollmentDateVar
                };
                return JSON.stringify(jsonStrObj);
            }
            // This method is used to create PUT Json request.
            function createPUTRequest(connToken, jsonObj, dbName, relName) {
                var putRequest = "{\n"
                        + "\"token\" : \""
                        + connToken
                        + "\","
                        + "\"dbName\": \""
                        + dbName
                        + "\",\n" + "\"cmd\" : \"PUT\",\n"
                        + "\"rel\" : \""
                        + relName + "\","
                        + "\"jsonStr\": \n"
                        + jsonObj
                        + "\n"
                        + "}";
                return putRequest;
            }
            function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
                var url = dbBaseUrl + apiEndPointUrl;
                var jsonObj;
                $.post(url, reqString, function (result) {
                    jsonObj = JSON.parse(result);
                }).fail(function (result) {
                    var dataJsonObj = result.responseText;
                    jsonObj = JSON.parse(dataJsonObj);
                });
                return jsonObj;
            }
            function resetForm() {
                $("#StudentRollno").val("")
                $("#studentName").val("");
                $("#studentClass").val("");
                $("#BirthDate").val("");
                $("#Address").val("");
                $("#EnrollmentDate").val("");
                $("#StudentRollno").focus();
            }
            function saveStudent() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "") {
                    return;
                }
                var putReqStr = createPUTRequest("90938259|-31949273451226700|90952578",
                        jsonStr, "SCHOOL-DB", "STUDENT-TABLE");
                alert(putReqStr);
                jQuery.ajaxSetup({async: false});
                var resultObj = executeCommand(putReqStr,
                        "http://api.login2explore.com:5577", "/api/iml");
                alert(JSON.stringify(resultObj));
                jQuery.ajaxSetup({async: true});
                resetForm();
            }
        </script>
    </body>
</html>
