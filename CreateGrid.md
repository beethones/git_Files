{------------------------------------------------------------------------------}
{    Regra responsável por: Cria grid ocorrênciaXTipo Equipamentos.            }
{    Programador responsável: Beethoven Nunes , Data Alteração: 28/12/2019     }
{    Engeman®                                                                  }
{------------------------------------------------------------------------------}
INTERFACE

IMPLEMENTATION

MAIN
  var
    sqlSelect, colunas, searchFields, parentDataset, dateFields : String; 
BEGIN
    sqlSelect := 'SELECT USER_CAXTIP.U_PK_REDUZIDO U_PK_REDUZIDO,                               '+chr(13)+
                 '    		 USER_CAXTIP.R_CAUSA_CODCAU R_CAUSA_CODCAU,                           '+chr(13)+
                 '   		 USER_CAXTIP.R_TIPAPLIC_CODEMP R_TIPAPLIC_CODEMP,                       '+chr(13)+
                 '   		 USER_CAXTIP.R_TIPAPLIC_CODTIPAPL R_TIPAPLIC_CODTIPAPL,                 '+chr(13)+
                 '   		 TIPAPLIC.TAG+" - "+TIPAPLIC.DESCRICAO AS TIP_APLIC                     '+chr(13)+
                 '                                                                              '+chr(13)+
                 '  FROM USER_CAXTIP                                                            '+chr(13)+
                 ' 	INNER JOIN TIPAPLIC ON USER_CAXTIP.R_TIPAPLIC_CODEMP=TIPAPLIC.CODEMP        '+chr(13)+
                 '                      AND USER_CAXTIP.R_TIPAPLIC_CODTIPAPL=TIPAPLIC.CODTIPAPL '+chr(13)+
                 '  WHERE USER_CAXTIP.R_CAUSA_CODCAU=:CODCAU ';

    colunas:= 'item width=90 FieldName="U_PK_REDUZIDO" Title.Caption="Reduzido" Title.Font.Color=ClGreen Title.Font.Style=[FsBold] Visible=false end '+
              'item width=100 FieldName="R_CAUSA_CODCAU" Title.Caption="Código Causa" Title.Font.Color=ClGreen Visible=false ReadOnly=true Title.Font.Style=[FsBold] end '+
              'item width=100 FieldName="R_TIPAPLIC_CODEMP" Title.Caption="Código Emp TipAplic" Title.Font.Color=ClGreen Visible=false ReadOnly=true Title.Font.Style=[FsBold] end '+
              'item width=100 FieldName="R_TIPAPLIC_CODTIPAPL" Title.Caption="Código TipAplic" Title.Font.Color=ClGreen Visible=false ReadOnly=true Title.Font.Style=[FsBold] end '+
              'item width=250 FieldName="TIP_APLIC" Title.Caption="Tipo de Aplicação" Title.Font.Color=ClBlue Title.Font.Style=[FsBold] end ';
  
    searchFields:= 'TIP_APLIC\TIPAPLIC=CODTIPAPL\TAG,DESCRICAO\CODTIPAPL=R_TIPAPLIC_CODTIPAPL,CODEMP=R_TIPAPLIC_CODEMP;';
    
    parentDataset:='CAUSA\CODCAU=R_CAUSA_CODCAU';
    
    dateFields:= 'U_PK_REDUZIDO=Reduzido;R_CAUSA_CODCAU=codCau;R_TIPAPLIC_CODEMP=CodEmp;R_TIPAPLIC_CODTIPAPL=codTipApl';    
  
    createGrid('PageGru', 'Tipo de Equipamento', 'CausaXTipAplic', colunas, 3, sqlSelect, true, true, true, parentDataset, searchFields, dateFields, false); 
END.