# ProjetoForms1.FrmClientes
Conectar clientes ao banco de dados sql

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace ProjetoForms1
{
    public partial class FrmClientes : Form
    {
        public FrmClientes()
        {
            InitializeComponent();
            ToolTip toolTip1 = new ToolTip();
            toolTip1.SetToolTip(txtCPF, "Campo Obrigatorio");
            ToolTip toolTip2 = new ToolTip();
            toolTip2.SetToolTip(txtNome, "Campo Obrigatorio");
            ToolTip toolTip3 = new ToolTip();
            toolTip3.SetToolTip(txtTelefone, "Campo Obrigatorio");
            ToolTip toolTip4 = new ToolTip();
            toolTip4.SetToolTip(txtCEP, "Campo Obrigatorio");
        }

  SqlConnection con = new SqlConnection(Dados.conexao);
        private string txtUF;

  private void FrmClientes_Load(object sender, EventArgs e)
        {

  }

  private void btnTeste_Click(object sender, EventArgs e)
        {
            //teste de conexão com o banco de dados
            try
            {
                con.Open();
                MessageBox.Show("Conexão realizada com sucesso!");
                con.Close();
            }
            catch (SqlException erro)
            {
                MessageBox.Show("Erro na conexão com o banco de dados: " + erro);
            }
        }

  private void btnInserir_Click(object sender, EventArgs e)
        {
            try
            {
                //validar os campos: cpf, nome,tel e cep.
                //se não estão preenchidos-enviar msgbox
                if (txtCPF.Text == "" || txtNome.Text == "" || txtTelefone.Text == string.Empty ||
                    txtCEP.Text == "") //ou||

  {
                    MessageBox.Show("Preencha todos os campos!", "Sistema TI35", MessageBoxButtons.OK,
                        MessageBoxIcon.Exclamation);
                }
                else
                {
                    //abrir a conexão
                    con.Open();
                    //comando sql para inserir dados na tabela
                    string sql = "insert into tbClientes (cpf,nome,telefone,cep,datanascimento,rua,numero,cidade,uf)" +
    "values ('" + txtCPF.Text + "','" +
    txtNome.Text + "','" + txtTelefone.Text + "','" + txtCEP.Text + "','" + txtDataNasc.Text + "','"
    + txtRua.Text + "','" + txtNumero.Text + "','" + txtCidade.Text + "','" + txtUF + "')";
                    //executar o comando sql
                    SqlCommand cmd = new SqlCommand(sql, con);
                    cmd.ExecuteNonQuery();
                    //fechar a conexão
                    con.Close();
                    MessageBox.Show("Cliente inserido com sucesso!");

  }
            }
            catch (SqlException erro)
            {
                MessageBox.Show("Erro ao inserir cliente: " + erro);
            }
        }

  private void label17_Click(object sender, EventArgs e)
        {

  }

  private void txtCPF_MaskInputRejected(object sender, MaskInputRejectedEventArgs e)
        {
            {
                //validar o cpf
                if (ValidaCPF.IsCpf(txtCPF.Text))
                {
                    lblCPF.Text = "CPF Válido";
                    lblCPF.ForeColor = Color.Green;
                }
                else
                {
                    lblCPF.Text = "CPF Inválido";
                    lblCPF.ForeColor = Color.Red;
                }
            }
        }
        /// <summary>
        /// Realiza a validação do CPF
        /// </summary>

private void label6_Click(object sender, EventArgs e)
        {

}

  private void DtPicker_ValueChanged(object sender, EventArgs e)
        {
            // Evento que é acionado quando o valor do DateTimePicker é alterado
            // Formata a data selecionada no formato desejado (ex: dd/MM/yyyy)
            txtDataNasc.Text = dtPicker.Value.ToString("dd/MM/yyyy");
        }
        // Evento que é acionado quando o valor do DateTimePicker é alterado
        private void dtPicker_ValueChanged(object sender, EventArgs e)
        {
            // Formata a data selecionada no formato desejado (ex: dd/MM/yyyy)
            txtDataNasc.Text = dtPicker.Value.ToString("dd/MM/yyyy");
        }

  // Evento do botão Confirmar (opcional)
        private void btnConfirmar_Click(object sender, EventArgs e)
        {
            // Atualiza o TextBox com a data selecionada no DateTimePicker
            txtDataNasc.Text = dtPicker.Value.ToString("dd/MM/yyyy");
        }
    }
}
