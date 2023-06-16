# Scheduling Policy to the Linux Kernel
Neste projeto nós iremos testar políticas de escalonamento e implementar uma nova no kernel do
linux. 
Com base na descrição apresentada, para o referido projeto deve ser apresentado os seguintes
itens:
- Descrever o funcionamento de um escalonamento;
- Criar um tutorial com exemplos de códigos para a criação de uma política de escalonamento
no linux;
- Apresente 4 políticas de escalonamento suportadas pelo kernel do linux;
- Depois de implementar sua política de agendamento e depurá-la com cuidado, você avaliará
seu desempenho executando combinações de processos intensivos de CPU em diferentes
políticas de agendamento e medindo o tempo necessário;
- Você pode usar o gettimeofday() para medir o tempo "wallclock" e getrusage()
para registrar o tempo do usuário e do sistema. Sua análise deve incluir wallclock,
sistema e tempo do usuário em milissegundos.
