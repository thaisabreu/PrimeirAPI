# PrimeirAPI

Solução simples para teste de API

* Projeto criado no VS 2019
* ASP.NET Core Web API
* Framework .NET Core 3.1
---------------------//------------------------------------------

* Packages instalados:
1) Microsoft.EntityFrameworkCore
2) Microsoft.EntityFrameworkCore.SqlServer (Erro motivador:  'DbContextOptionsBuilder' não contém uma definição para 'UseSqlServer')
3) Microsoft.EntityFrameworkCore.Tools (Erro motivador: The term 'Add-Migration' is not recognized as the name of a cmdlet, function, script file, or operable program)
	Usado para os comandos do gerenciador de pacotes no Visual Studio e linha de comando.
4) Microsoft.Bcl.AsyncInterfaces (Erro Motivador: 'Could not load file or assembly 'Microsoft.Bcl.AsyncInterfaces, Version=1.0.0.0)
---------------------//-----------------------------------------
1. Criar pasta Modelo
1.1 Criar classe Fornecedor (modelo de dados)
1.3 Criar classe ApiDbContext (classe principal, responsável por mapear os modelos ligados na tabela de dados)

2. Adicionar o ConnectionString:
2.1 Abrir arquivo: appsettings.json
2.3 Adicionar Connection:
	  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=PrimeiraAPI;Trusted_Connection=True;MultipleActiveResultSets=true"
  }

3. Adicionar configurar de banco na classe Startup:
3.1 Abrir classe Startup
3.4 adicionar:
	services.AddDbContext<ApiDbContext>(optionsAction: options =>
                options.UseSqlServer(Configuration.GetConnectionString(name:"DefaultConnection")));

4. Abrir classe ApiDbContext 
4.1 adicionar o construtor
	 public ApiDbContext(DbContextOptions options) : base(options)
        {

        }
4.2 adionar modelos de dados utilizando o DbSet
	public DbSet<Fornecedor> Fornecedores { get; set; }

5. Adicionar Migration (PM> Add-Migration Inicial -Verbose)
6. Update data base - Aplicar o migration criado  (PM> update-database)
   Essa hora é criado o database PrimeiraAPI e a coluna Fornecedores

7. Criar na pasta Controller com o botão direito > add > controller 
7.1 Escolher a opção "API Controller with actions, using Entity Framework" 
--- Criar o controller Fornecedores. 
**** Gerou erro onde precisei adicionar o package 4
**** Após gerou o erro: The database provider attempted to register an implementation of the 'IRelationalTypeMappingSource' service
     Solução:Deixei meus package abaixo tudo na mesma versão
	Microsoft.EntityFrameworkCore 3.1.15
	Microsoft.EntityFrameworkCore.SqlServer 3.1.15
	Microsoft.EntityFrameworkCore.Tools 3.1.15

8. Adicionar dados no banco
8.1 Abrir no VS > SQL Server Object Explorer > (localdb) > DataBase > PrimeiraAPI
8.2 Clicar com botão direito na tabela "Fornecedores" > View Data
8.3 Gerar ID GUID: Tools > Create GUID > Opcional a forma que vai escolher, escolhe a 4
8.3.1 Clicar em "Copy" e colocar na coluna "Id"
8.4 Preencher o restante dos dados
8.5 Executar a aplicação/controller e verificar se estar retornando 

--------------------------------------------\\-------------------------------


