Imports System.Data
Imports System.Data.OleDb
Public Class Form1

    Public con As New OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\HP\Desktop\net\SATTU_NET\Database1.mdb")
    'FUNCTION 
    Public Sub loadData()

        Dim newCon As New OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\HP\Desktop\net\SATTU_NET\Database1.mdb")
        Dim query As String = "select * from student"
        Dim adpter As New OleDbDataAdapter(query, newCon)


        Dim table As New DataTable
        adpter.Fill(table)

        DataGridView1.DataSource = table

    End Sub
    'FUNCTIO.
    Public Sub searchInserted()
        Dim names As String = TextBox2.Text
        Dim ages As String = 0

        Dim insertQuery As String = "insert into student (name,age) values( @name, @age)"
        Dim cmd As New OleDbCommand(insertQuery, con)

        cmd.Parameters.AddWithValue("@name", names)
        cmd.Parameters.AddWithValue("@age", ages)

        con.Open()
        cmd.ExecuteNonQuery()
        con.Close()
        loadData()
        MessageBox.Show(" added successfully...")
        clear()

    End Sub
    'FUNCTION
    Public Sub clear()
        TextBox1.Clear()
        TextBox2.Clear()
        TextBox3.Clear()
    End Sub

    


    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        loadData()
    End Sub

    Private Sub Button3_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles DELETE_BTN.Click
        Dim query As String = "delete from student where id=@id"
        Dim cmd As New OleDbCommand(query, con)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)

        con.Open()
        Dim count As Integer = cmd.ExecuteNonQuery()
        con.Close()
        clear()
        loadData()
        MessageBox.Show(count & " delted succesffullyy.")
    End Sub

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles INSERT_BTN.Click
        Dim insertQuery As String = "insert into student (id,name,age) values(@id, @name, @age)"
        Dim cmd As New OleDbCommand(insertQuery, con)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)
        cmd.Parameters.AddWithValue("@name", TextBox2.Text)
        cmd.Parameters.AddWithValue("@age", TextBox3.Text)

        con.Open()
        Dim count As Integer = cmd.ExecuteNonQuery()
        con.Close()
        MessageBox.Show(count & " inserted records successfully...")
        clear()
        loadData()
    End Sub
   
  
  
    Private Sub Button6_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles EXIT_BTN.Click
        End
    End Sub

    Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles UPDATE_BTN.Click
        Dim update As String = "update student set  name=@name,age=@age where id=@id"
        Dim cmd As New OleDbCommand(update, con)

        cmd.Parameters.AddWithValue("@name", TextBox2.Text)
        cmd.Parameters.AddWithValue("@age", TextBox3.Text)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)

        con.Open()
        Dim count As Integer = cmd.ExecuteNonQuery()
        con.Close()
        loadData()
        MessageBox.Show(count & "updated record succesfully...")
        clear()

    End Sub

    Private Sub Button4_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SEA_BY_ID.Click
        Dim query As String = "select * from student where id=@id"
        Dim cmd As New OleDbCommand(query, con)

        cmd.Parameters.AddWithValue("@id", TextBox1.Text)

        Dim adpater As New OleDbDataAdapter(cmd)
        Dim table As New DataTable
        adpater.Fill(table)

        If table.Rows.Count > 0 Then
            TextBox2.Text = table.Rows(0)(1).ToString()
            TextBox3.Text = table.Rows(0)(2).ToString()
            MessageBox.Show("data fetch successfully...")
        Else
            MessageBox.Show("data not fetched...")
        End If
    End Sub

    Private Sub Button7_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SER_BY_NAME.Click
        Dim query As String = "select * from student where name=@name"
        Dim cmd As New OleDbCommand(query, con)

        cmd.Parameters.AddWithValue("@name", TextBox2.Text)

        Dim adpater As New OleDbDataAdapter(cmd)
        Dim table As New DataTable
        adpater.Fill(table)

        If table.Rows.Count > 0 Then
            TextBox1.Text = table.Rows(0)(0).ToString()
            TextBox3.Text = table.Rows(0)(2).ToString()
            MessageBox.Show("data fetch successfully...")
        Else
            searchInserted()
        End If
    End Sub


    Private Sub Button8_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles INCRE_BY_ONE.Click
        Dim query As String = "update student set age=age+1 where id=@id"
        Dim cmd As New OleDbCommand(query, con)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)

        con.Open()
        cmd.ExecuteNonQuery()
        con.Close()
        loadData()
        MessageBox.Show("updated data successfully...")
    End Sub

    Private Sub Button9_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ASC_BTN.Click
        Dim newCon As New OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\HP\Desktop\net\SATTU_NET\Database1.mdb")
        Dim query As String = "select * from student order by id ASC"
        Dim adpter As New OleDbDataAdapter(query, newCon)


        Dim table As New DataTable
        adpter.Fill(table)

        DataGridView1.DataSource = table
    End Sub

    Private Sub Button10_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles DSC_BTN.Click
        Dim newCon As New OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\HP\Desktop\net\SATTU_NET\Database1.mdb")
        Dim query As String = "select * from student order by id DESC"
        Dim adpter As New OleDbDataAdapter(query, newCon)


        Dim table As New DataTable
        adpter.Fill(table)

        DataGridView1.DataSource = table
    End Sub

    Private Sub Button5_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CLEAR_BTN.Click
        clear()
          End Sub

End Class
===========================================================================================================================================
          body {
        margin: 0px;
        padding: 0;
        background-color: cornflowerblue;
    }

    ul {
        list-style-type: none;
        text-decoration: none;
        align-items: center;
        overflow: hidden;
        margin: 0;
        padding: 0;
        background-color: black;
    }

    li {
        float: right;
    }

    li a {
        color: white;
        display: block;
        margin: 12px;
        padding: 14px;
        text-decoration: none;
    }


    <script>
    let xhr=new XMLHttpRequest();   
    xhr.open("GET", "products.json", true);
    xhr.onreadystatechange=function(){
        if(xhr.readyState==4&&xhr.status==200){
            let val1=JSON.parse(xhr.responseText);
            let val2=document.querySelector("#tablechaghe")
            let out="";
            for(let val3 of val1){
                out+=`
                <tr>
                    <td>${val3.id}</td>
                    <td> <img src='${val3.image}'> </td>
                    <td>${val3.name}</td>
                    <td>${val3.price}</td>
                    <td>${val3.inventory}</td>
                    <td>${val3.productCode}</td>

                    </tr>`;
            }val2.innerHTML=out;
        }
    };
    xhr.send();
</script>


[
    {
       "id": 1,
       "image": "",
       "name": "Orient Vita Pro 28\"",
       "price": "284.00",
       "inventory": 4,
       "productCode": "K203"
    },
    {
       "id": 2,
       "image": "",
       "name": "Orient S-400 26\"",
       "price": "198.00",
       "inventory": 14,
       "productCode": "K433"
    },
    {
       "id": 3,
       "image": "",
       "name": "Bullet Bora 20\"",
       "price": "350.00",
       "inventory": 7,
       "productCode": "K012"
    },
    {
       "id": 4,
       "image": "",
       "name": "Feder handmade",
       "price": "790.00",
       "inventory": 5,
       "productCode": "G0127"
    },
    {
       "id": 5,
       "image": "",
       "name": "Ibanez G120",
       "price": "430.00",
       "inventory": 2,
       "productCode": "G1233"
    },
    {
       "id": 6,
       "image": "",
       "name": "Feder Blues edition",
       "price": "650.00",
       "inventory": 6,
       "productCode": "G4478"
    }
 ]
  

