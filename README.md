# correios-zpl-js
Um módulo node para impressão de etiquetas dos correios em impressoras Zebra (rede ou USB) usando a linguagem ZPL II.

# Pré-Requisitos

As fontes Arial e ArialBold precisam estar instaladas na impressora e devem ter os nomes ARI000.FNT e ARI001.FNT respectivamente.

Para instalar fontes na impressora será necessário seguir as instruções deste link:

[Instalação de Fontes em Impressoras Zebra](https://www.zebra.com/us/en/support-downloads/knowledge-articles/zebra-setup-utilities--downloading-fonts-to-a-printer.html)

Link para instalar o Zebra Setup Utility (somente Windows) siga as instruções:

[Instalar o Zebra Setup Utility](https://www.zebra.com/us/en/products/software/barcode-printers/zebralink/zebra-setup-utility.html)

# Exemplo de uso (o objeto obj.options preparado para impressora de rede):
```
const CorreiosZPL = require("../index");

const ZPL_CUSTOM_LOGO = `^GFA,7200,7200,30,,:::::::::::::::::::::::gM01F,gM01FC,gM01FF,gM01FF8,gM01FFC,gM01FFE,g01EK01IF,g03FK01IF8,g0FF8J01IF8,Y01FFCJ01IFC,Y03FFEJ01IFC,Y03IFJ01IFC,Y01IF8I01IFE,g0IFCI01IFE,g07FFEI01IFE,g03IFI01IFE,g01IF8001IFE,gG0IFC001IFE,W03I07FFE001IFE,W078003IF001IFC,W0FC001IF801IFC,W0FEI0IFC01IFC,V01FFI07FFE01IF8,V03FF8003IF01IF8,V03FFC001IF81IF,V03FFEI0IFC1FFE,V01IFI07FFE1FFE,W0IF8003IF1FF8,W07FFC001IF9FF,W03FFEI0IFDFC,W01IFI07JF,X0IF8003LF8,X07FFC001LFE,X03FFEI0LFE,X01IFI07LF8,U02I0IF8003LF8,U07I07FFC003LFE,U07I03FFE003MF,U078001IF003MF8,U07CI0IF003MFC,U07FI07FF003FF00C008,U0FF8003FF003FE004,U0FF8001FF003FE006,U0FFC001FF003FE007,U0FFE001FF003FE0078,U0IF801FF003FE007C,U0IFC01FF003FE007E,U07FFC01FF003FE007F,U03IF01FF003FE007F8,U01IF81FF003FE007FC,V0IF81FF003FE007KF,V07FFC1FF003FE007FCIF8,V03FFE1FF003FE007FC7FFC,V01IF1FF003FE007FC3FFE,W0IF9FF003FE007FC1IF,W07KF003FE007FC0IF8,W03KF003FE007FC07FFC,W01KF003FE007FC03FFE,X0KF003FE007FC01IF,X07JF003FE007FC01801,X03JF003FE007FC018,U0C001JF003FE007FC01C,U0EI0JF003FE007FC00E,U0FI07IF003FE007FC01F,U0F8003IF003FE007FC00F8,U0FC001IF003FE007FC00FC,U0FEI0IF003FE007FC00FE,U0FFI07FF003FE007FC00FF,U0FF8003FF003FE007FC00FF8,U0FFC001FF003FE007FC00FF8,U0FFEI0FF003FE007FC00FF8,U0IFI07F003FE007FC00FF8,U0IF8003F003FE007FC00FF8,U0IFC003F003FE007FC00FF8,U07FFEI0F003FE007FC00FF801FF,U03IFI0F003FE007FC00FF803FF8,U01IF8003003FE007FC00FF803FFC,V0IFC003003FE007FC00FF803FFE,V07FFE001003FE007FC00FF803IF,V03IFK03FE007FC00FF803IFC,V01IF8J03FE007FC00FF803IFE,W0IFCJ03FE007FC00FF803JF,W07FFEJ03FE007FC00FF803JF8,W03IFJ03FE007FC00FF803JFC,W01IF8I03FF007FC01FF801JFE,X0IFCI03FF007FC00FF803KF,X07FFEI03FF8N07MF,X03IFI03FFCN07MF,X01IF8003FFEN07MF,Y0IFC001IFN07MF,Y07FFEI0IFCM03MF,Y03IFI07FFEM03LFE,Y01IF8003FFEM03LFE,g0IFC001IF8L01LFC,g07FFEI0IF8M0LFC,g03IFI07FF8M0LF8,g01IF8003FF8M07KF,gG0IFC001FF8M03JFE,gG07FFEI0FF8M01JFC,gG03IFI07F8N07IF8,gG01IF8003F8N01FFE,gH0IFC001F8O03E,gH07FFEI0F8,gH03IFI078,gH01IF80038,gI0IFC0018,gI07FFEI08,gI03IF,gI01IF8,gJ0IFC,gJ07FFE,gJ03IF,gJ01IF8,gK0IFC,gK07FFE,gK03IF,gK01IF8,gL0IFC,gL07FFE,gL03IF,gL01IF8,gM0IF8,gM07FF8,gM03FF8,gM01FF8,gN0FF8,gN07F8,gN03F8,gN01F8,gO0F8,gO078,gO038,gO018,,:::::::::::::::::::::::::::::V0JFE3IFC3IF803IFJ07FE,V0JFE3IFE3JF03IFEI07FE,U01JFC3IFE3JF83JFI07FE,U01JFC3IFE3JFC3JF800IF,U03JF83IFE3JFC3JFC00IF,U03JF83IFC3F8FFE3JFE00IF,X0FF03F8003F81FE3F83FE01IF8,X0FF03F8003F81FE3F81FE01IF8,W01FE03F8003F81FE3F80FE01IF8,W03FE03F8003F81FE3F80FE03IFC,W03FC03F8003F81FC3F80FE03F9FC,W07FC03F8003F83FC3F80FE03F9FC,W07F803IFE3JF83F81FE07F9FE,W0FF803IFE3JF03F83FE07F1FE,W0FF003IFE3IFE03JFC07F0FE,V01FE003IFE3JF03JFC0FF0FF,V01FE003IFE3JF83JF80FE0FF,V03FC003IFC3F87FC3JF00FE0FF,V03FC003F8003F81FE3IFC01KF8,V07F8003F8003F80FE3FBFC01KF8,V07F8003F8003F80FE3FBFE01KF8,V0FFI03F8003F80FE3F9FE03KFC,V0FFI03F8003F80FE3F9FF03KFC,U01FF7FC3IFC3F81FE3F8FF83FEIFC,U01JFC3IFE3JFE3F87F87F801FE,U03JF83IFE3JFC3F87FC7F001FE,U03JF83IFE3JFC3F83FC7FI0FE,U07JF03IFE3JF83F83FE7FI0FF,U0JFE03IFE3IFE03F81JFI0FF,,:::::::::::::::::::::::`;

const correiosZpl = new CorreiosZPL();

const obj = {
  // Configuration
  options: {
    printerType: "N",               // Mude para "U" se necessita impressão pela USB
    printerAddress: "<IP or URL>",  // Obrigatório somente para impressoras de rede
    printerPort: 9100,              // Opcional, 9100 por padrão, somente para impressoras de rede
    timeout: 30000,                 // Opcional, 30000 por padrão, somente para impressoras de rede
    printerName: "<PrinterName>",   // Obrigatório somente para impressoras USB
    workDir: "./tmp",               // Opcional, define o local de criação de arquivos temporários 
    customLogoZpl: ZPL_CUSTOM_LOGO, // Imagem em formato ZPL do logo da sua empresa, opcional
    darknessLevel: 20,              // Opcional, escurece a etiqueta
  },
  // Label informations
  label: {
    trackNumber: "OJ333333333BR",     // Código da etiqueta completo
    postCard: "1234567890",           // Seu código de cartão de postagem dos correios
    serviceCode: "04162",             // Código do serviço dos correios (consultar o manual do SIGEP)
    serviceName: "SEDEX",             // SEDEX, SEDEX 10, SEDEX 12, SEDEX HOJE, PAC ou CARTA
    weight: 100,                      // Peso do pacote, opcional
    plp: "307273555",                 // Número da PLP, opcional 
    contract: "9999999999",           // Número do contrato com o cliente, opcional
    invoice: "10000",                 // Número da nota fiscal, opcional
    invoiceValue: "100.00",           // Valor da nota fiscal, opcional
    remarks: "",                      // Observações, opcional
    services: {
      inHands: true,                  // Mãos Próprias, opcional, serviço 002
      receiptNotice: false,           // Aviso de Recebimento, opcional, serviço 001
      declaredValue: true,            // Valor declarado nacional, serviço 019
      neighborDelivery: false,        // Entrega no vizinho, opcional, serviço 011
      largeFormats: false,            // Grandes Formatos, opcional, serviço 057
    },
    sender: {                         // Dados do remetente
      name: "Empresa de teste de impressão de etiquetas",
      address: "Av. Presidente Vargas",
      addressNumber: 8001,      
      complement: "Torre A sala 333",
      neighborhood: "Centro",
      city: "Rio de Janeiro",
      state: "RJ",
      zipCode: "21091751",
      phone: "21123451234",
    },
    recipient: {                      // Dados do destinatário
      name: "Empresa Destinatário",
      careOf: "Sra. Fulana de Tal",
      address: "Rua do Destinatário",
      addressNumber: 444,
      complement: "Sala 2",
      neighborhood: "Jardim das Aroeiras",
      city: "Piauí",
      state: "PI",
      zipCode: "99770490",
      phone: "99123451234",
    },
  },
};

try {
  correiosZpl.zplCode(obj);
  correiosZpl.printLabel(obj);
} catch (err) {
  console.log(err);
}
```
# Carregar uma imagem PNG para usar como logo da empresa (conversão para ZPL):

Na construção do objeto use a função convertPngToZplImage (melhores resultados são obtidos com imagens de até 240 pixels horizontais):
```
...
customLogoZpl: correiosZpl.convertPngToZplImage(<path_to_png_image>);
...
```

# Impressão de código ZPL (para imprimir outras etiquetas):

De posse do seu próprio código ZPL, ao invés de chamar o método correiosZpl.printLabel(obj), execute:

```
correiosZpl.printLabel(obj, zplInstructions);
```

Onde Obj contém a parte inicial do objeto de exemplo acima (obj.options) e zplInstructions contém a listagem de instruções ZPL.

# Instruções ZPL

Se deseja montar sua própria etiqueta, sugiro começar pelo criador online de etiquetas (Labelary):

[Labelary](http://labelary.com/viewer.html)

Segue um link com instruções iniciais sobre o ZPL II:

[ZebraMaster](http://zebramaster.blogspot.com/2013/04/linguagem-de-programacao-zebra-zpl.html)

Lista completa de instruções ZPL:

[ZPL Programming](https://www.zebra.com/content/dam/zebra/manuals/printers/common/programming/zpl-zbi2-pm-en.pdf)

