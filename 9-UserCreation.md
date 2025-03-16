db.createUser({
    user:"testuser",
    pwd:passwordPrompt(),
    customData:{movieId: 12345},
    roles:[
        { role: "clusterAdmin",db:"admin"},
        { role: "readAnyDatabase",db:"admin"},
        "readWrite"
    ]
},
{w:"majority", wtimeout:5000})


clusterAdmin => grant full admin rights for entire cluster


db.getUsers() => to get all users

db.dropUser("testuser", {w:"majority", wtimeout:5000})

db.changeUserPassword("testUser", passwordPrompt())

update user => 

db.updateUser("testUser",{
     roles:[
        { role: "readWrite", db:"myDatabase"},
    ]
})


Summary of Key Commands

Create User=>	db.createUser({...})
List Users =>	db.getUsers()
Change Password	=>db.changeUserPassword("user", "newpassword")
Modify Roles=>	db.updateUser("user", { roles: [...] })
Grant Role=>	db.grantRolesToUser("user", [{ role: "role", db: "db" }])
Revoke Role= >	db.revokeRolesFromUser("user", [{ role: "role", db: "db" }])
Unlock User(Reset Password)=>	db.changeUserPassword("user", "newpassword")
Kill a Session=>	db.killOp(opid)
Delete User	=>db.dropUser("user")
