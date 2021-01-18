please download the file for better understanding of the syntax
payload syantax: 1,<payload>,2 from <whereevr>
reasons for using group_concat:
    so i will be discussing the uses of group_concat and concat and concat_ws which are mainly used in mysql
    concat: return the only one value required 
    suppose if we use concat(table_name) in the backend which is in the information_schema.tables we will be getting the name of only one table
    suppose if we use concat_ws we need to specify the specifier which will help in concating the given attributes of the one user
  unlike these we have group_concat which helps in concating the whole thing at once
  
 
