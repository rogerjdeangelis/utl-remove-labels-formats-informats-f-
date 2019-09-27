# utl-remove-labels-formats-informats-f-
Remove labels formats informats from all tables in a library 

    Remove labels formats informats from all tables in a library                                                                
                                                                                                                                
    github                                                                                                                      
    https://tinyurl.com/y4a4avph                                                                                                
    https://github.com/rogerjdeangelis/utl-remove-labels-formats-informats-from-all-tables-in-a-library                         
                                                                                                                                
    SAS  Forum                                                                                                                  
    https://tinyurl.com/y2dx6664                                                                                                
    https://communities.sas.com/t5/SAS-Programming/How-can-i-remove-formats-and-informats-for-all-datasets-in-a/m-p/591809      
                                                                                                                                
    macros                                                                                                                      
    https://tinyurl.com/y9nfugth                                                                                                
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                  
                                                                                                                                
    *_                   _                                                                                                      
    (_)_ __  _ __  _   _| |_                                                                                                    
    | | '_ \| '_ \| | | | __|                                                                                                   
    | | | | | |_) | |_| | |_                                                                                                    
    |_|_| |_| .__/ \__,_|\__|                                                                                                   
            |_|                                                                                                                 
    ;                                                                                                                           
                                                                                                                                
    proc datasets lib=work kill;                                                                                                
    run;quit;                                                                                                                   
                                                                                                                                
    data one two tre;                                                                                                           
       set sashelp.stocks(keep=ADJCLOSE CLOSE DATE obs=30);                                                                     
       label ADJCLOSE =  "Market ADJCLOSE "                                                                                     
             CLOSE    =  "Market CLOSE    "                                                                                     
             DATE     =  "Market DATE     "                                                                                     
       ;                                                                                                                        
       select ;                                                                                                                 
            when (mod(_n_,3)=0) output one;                                                                                     
            when (mod(_n_,4)=0) output two;                                                                                     
            when (mod(_n_,5)=0) output tre;                                                                                     
            otherwise;                                                                                                          
       end;                                                                                                                     
    run;quit;                                                                                                                   
                                                                                                                                
    Three SAS Tables                                                                                                            
    ================                                                                                                            
                                                                                                                                
             Member                                                                                                             
    #  Name  Type       File Size  Last Modified                                                                                
                                                                                                                                
    1  ONE   DATA           128KB  09/27/2019 06:26:29                                                                          
    2  TRE   DATA           128KB  09/27/2019 06:26:29                                                                          
    3  TWO   DATA           128KB  09/27/2019 06:26:29                                                                          
                                                                                                                                
                                                                                                                                
    WORK.ONE WORK.TWO WORK.TRE                                                                                                  
    ==========================                                                                                                  
       Alphabetic List of Variables and Attributes                                                                              
                                                                                                                                
    #    Variable    Type    Len    Format       Informat    Label                                                              
                                                                                                                                
    3    ADJCLOSE    Num       8    DOLLAR8.2    BEST32.     Market DATE                                                        
    2    CLOSE       Num       8    DOLLAR8.2    BEST32.     Market CLOSE                                                       
    1    DATE        Num       8    DATE.        DATE.       Market ADJCLOSE                                                    
                                                                                                                                
    *            _               _                                                                                              
      ___  _   _| |_ _ __  _   _| |_                                                                                            
     / _ \| | | | __| '_ \| | | | __|                                                                                           
    | (_) | |_| | |_| |_) | |_| | |_                                                                                            
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                           
                    |_|                                                                                                         
    ;                                                                                                                           
                                                                                                                                
    WORK.ONE WORK.TWO WORK.TRE                                                                                                  
    ==========================                                                                                                  
                                                                                                                                
     Variables in Creation Order                                                                                                
                                                                                                                                
    #    Variable    Type    Len                                                                                                
                                                                                                                                
    1    DATE        Num       8                                                                                                
    2    CLOSE       Num       8                                                                                                
    3    ADJCLOSE    Num       8                                                                                                
                                                                                                                                
    *                                                                                                                           
     _ __  _ __ ___   ___ ___  ___ ___                                                                                          
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                         
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                         
    | .__/|_|  \___/ \___\___||___/___/                                                                                         
    |_|                                                                                                                         
    ;                                                                                                                           
                                                                                                                                
    ods select members;                                                                                                         
    ods output members=dsns;                                                                                                    
      proc contents data=work._all_ mt=data;                                                                                    
      run;quit;                                                                                                                 
    ods output close;                                                                                                           
                                                                                                                                
    proc sql;                                                                                                                   
     select name into :nams1- from dsns                                                                                         
    ;quit;                                                                                                                      
    %let namsn=&sqlobs;                                                                                                         
                                                                                                                                
                                                                                                                                
    proc datasets lib=work mt=data;                                                                                             
      %do_over(nams,phrase=%str(                                                                                                
                                                                                                                                
         modify ?;                                                                                                              
                                                                                                                                
          attrib _all_                                                                                                          
          label='';                                                                                                             
          format _all_;                                                                                                         
          informat _all_;                                                                                                       
      ));                                                                                                                       
                                                                                                                                
    run;quit;                                                                                                                   
                                                                                                                                
                                                                                                                                
