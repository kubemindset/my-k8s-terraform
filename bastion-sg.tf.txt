module "vpc" {
  source = "./module/vpc"
  region               = var.region
  vpc_cidr             = var.vpc_cidr
  public_subnet_cidr   = var.public_subnet_cidr
  private_subnet1_cidr = var.private_subnet1_cidr
  private_subnet2_cidr = var.private_subnet2_cidr
  az1                  = var.az1
  az2                  = var.az2
}
resource "aws_security_group" "bastion_sg" {
  name        = "bastion-host-sg"
  description = "Security Group for Bastion Host in public subnet"
  vpc_id      = module.vpc.vpc_id
  depends_on = [module.vpc]  # <- Explicit dependency on VPC module
}

# Inbound Rule: Allow all traffic (for SSH and testing, restrict in production)
resource "aws_security_group_rule" "bastion_inbound" {
  type              = "ingress"
  from_port         = 0
  to_port           = 0
  protocol          = "-1"  # -1 means all protocols
  cidr_blocks       = ["0.0.0.0/0"]
  security_group_id = aws_security_group.bastion_sg.id
}

# Outbound Rule: Allow all traffic
resource "aws_security_group_rule" "bastion_outbound" {
  type              = "egress"
  from_port         = 0
  to_port           = 0
  protocol          = "-1"  # All protocols
  cidr_blocks       = ["0.0.0.0/0"]
  security_group_id = aws_security_group.bastion_sg.id
}