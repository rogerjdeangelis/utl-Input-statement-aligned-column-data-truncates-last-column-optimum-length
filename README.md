# utl-Input-statement-aligned-column-data-truncates-last-column-optimum-length
Input statement aligned column data truncates last column 

    Input statement aligned column data truncates last column                                                                   
                                                                                                                                
    github                                                                                                                      
    https://tinyurl.com/y6r8z7ob                                                                                                
    https://github.com/rogerjdeangelis/utl-Input-statement-aligned-column-data-truncates-last-column-optimum-length             
                                                                                                                                
    SAS Forum                                                                                                                   
    https://tinyurl.com/yyhl4k5y                                                                                                
    https://communities.sas.com/t5/SAS-Programming/Input-statement-aligned-column-data-truncates-last-column/m-p/591539         
                                                                                                                                
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
                                                                                                                                
    data have;                                                                                                                  
          input Fiscal $ 1-16 Marca $ 17-36                                                                                     
                AssetTypeSegment $ 37-60 Brand $ 61-73;                                                                         
          infile datalines expandtabs truncover firstobs=2;                                                                     
          datalines;                                                                                                            
    Fiscal            Marca                      Segment                       Brand                                            
    ACCESORIOS        ACCESORIOS                 Non-Automotive                Not Defined                                      
    ;                                                                                                                           
    run;                                                                                                                        
                                                                                                                                
    * Here is the issue Brand is missing;                                                                                       
    Up to 40 obs WORK.HAVE total obs=1                                                                                          
                                                                                                                                
    Obs      FISCAL        MARCA       ASSETTYPESEGMENT    BRAND                                                                
                                                                                                                                
     1     ACCESORIOS    ACCESORIOS     Non-Automotive                                                                          
                                                                                                                                
    *          _       _   _                                                                                                    
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                         
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                        
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                       
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                       
                                                                                                                                
    ;                                                                                                                           
                                                                                                                                
    Simplify the code and                                                                                                       
    Highlight the datastep and type 'cuth' on the classic editor clean command line.                                            
                                                                                                                                
    This realigns the input;                                                                                                    
                                                                                                                                
    data have;                                                                                                                  
       informat Fiscal Marca AssetTypeSegment Brand $32.;                                                                       
       input Fiscal Marca AssetTypeSegment Brand & ;                                                                            
    cards4;                                                                                                                     
    Fiscal Marca Segment Brand                                                                                                  
    ACCESORIOS ACCESORIOS Non-Automotive Not Defined                                                                            
    ;;;;                                                                                                                        
    run;                                                                                                                        
                                                                                                                                
    or                                                                                                                          
                                                                                                                                
    data have;                                                                                                                  
       informat Fiscal Marca AssetTypeSegment Brand $32.;                                                                       
       input Fiscal & Marca & AssetTypeSegment & Brand & ;                                                                      
    cards4;                                                                                                                     
    Fiscal            Marca                      Segment                       Brand                                            
    ACCESORIOS        ACCESORIOS                 Non-Automotive                Not Defined                                      
    ;;;;                                                                                                                        
    run;                                                                                                                        
                                                                                                                                
          Variables in Creation Order                                                                                           
                                                                                                                                
    Variable            Type    Len    Informat                                                                                 
                                                                                                                                
    FISCAL              Char     32    $32.                                                                                     
    MARCA               Char     32    $32.                                                                                     
    ASSETTYPESEGMENT    Char     32    $32.                                                                                     
    BRAND               Char     32    $32.                                                                                     
                                                                                                                                
                                                                                                                                
    If you want to optimize the lengths of variable                                                                             
                                                                                                                                
    %utl_optlen(inp=have,out=have);                                                                                             
                                                                                                                                
           Variables in Creation Order                                                                                          
                                                                                                                                
     Variable            Type    Len                                                                                            
                                                                                                                                
     FISCAL              Char     10                                                                                            
     MARCA               Char     10                                                                                            
     ASSETTYPESEGMENT    Char     14                                                                                            
     BRAND               Char     11                                                                                            
                                                                                                                                
