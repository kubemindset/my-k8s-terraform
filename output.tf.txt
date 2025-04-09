output "bastion_sg_id" {
  description = "The ID of the Bastion Host Security Group"
  value       = aws_security_group.bastion_sg.id
}

output "vpc_id" {
  description = "The ID of the created VPC"
  value       = module.vpc.vpc_id
}