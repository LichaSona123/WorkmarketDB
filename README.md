-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`Profesional`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Profesional` (
  `idProf` INT NOT NULL AUTO_INCREMENT,
  `usuario` VARCHAR(45) NOT NULL,
  `contrasena` VARCHAR(45) NOT NULL,
  `nombre` VARCHAR(45) NOT NULL,
  `apellido` VARCHAR(45) NOT NULL,
  `telefono` INT NOT NULL,
  `email` VARCHAR(45) NOT NULL,
  `fotoPerfil` VARCHAR(45) NOT NULL,
  `tituloProfesional` VARCHAR(45) NULL,
  `calificacion` INT NOT NULL,
  `curriculum` VARCHAR(45) NOT NULL,
  `direccion` VARCHAR(45) NOT NULL,
  `localidad` VARCHAR(45) NOT NULL,
  `provincia` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idProf`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`PublicacionP`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`PublicacionP` (
  `idPublicacionP` INT NOT NULL AUTO_INCREMENT,
  `rubro` VARCHAR(45) NULL,
  `titulo` VARCHAR(45) NULL,
  `descripcion` VARCHAR(45) NOT NULL,
  `idProf` INT NOT NULL,
  PRIMARY KEY (`idPublicacionP`, `idProf`),
  INDEX `idProf_idx` (`idProf` ASC) VISIBLE,
  CONSTRAINT `idProf`
    FOREIGN KEY (`idProf`)
    REFERENCES `mydb`.`Profesional` (`idProf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Empresa`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Empresa` (
  `idEmpresa` INT NOT NULL AUTO_INCREMENT,
  `usuario` VARCHAR(45) NOT NULL,
  `contrasena` VARCHAR(45) NOT NULL,
  `razonSocial` VARCHAR(45) NOT NULL,
  `tel` INT NOT NULL,
  `email` VARCHAR(45) NOT NULL,
  `direccion` VARCHAR(45) NOT NULL,
  `localidad` VARCHAR(45) NOT NULL,
  `provincia` VARCHAR(45) NOT NULL,
  `rubro` VARCHAR(45) NOT NULL,
  `logo` VARCHAR(45) NULL,
  `calificacion` INT NULL,
  `certificacion` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idEmpresa`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`publicacionE`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`publicacionE` (
  `idpublicacionE` INT NOT NULL AUTO_INCREMENT,
  `descripcion` VARCHAR(45) NULL,
  `titulo` VARCHAR(45) NOT NULL,
  `requisitos` VARCHAR(45) NOT NULL,
  `idEmpresa` INT NOT NULL,
  PRIMARY KEY (`idpublicacionE`, `idEmpresa`),
  INDEX `idEmpresa_idx` (`idEmpresa` ASC) VISIBLE,
  CONSTRAINT `idEmpresa`
    FOREIGN KEY (`idEmpresa`)
    REFERENCES `mydb`.`Empresa` (`idEmpresa`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Profesional-publicacionE`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Profesional-publicacionE` (
  `idProfesional` INT NOT NULL,
  `idPublicacionE` INT NOT NULL,
  PRIMARY KEY (`idProfesional`, `idPublicacionE`),
  INDEX `idPublicacionE_idx` (`idPublicacionE` ASC) VISIBLE,
  CONSTRAINT `idProf`
    FOREIGN KEY (`idProfesional`)
    REFERENCES `mydb`.`Profesional` (`idProf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `idPublicacionE`
    FOREIGN KEY (`idPublicacionE`)
    REFERENCES `mydb`.`publicacionE` (`idpublicacionE`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Profesional-Empresa`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Profesional-Empresa` (
  `idProf` INT NOT NULL,
  `idEmpresa` INT NOT NULL,
  PRIMARY KEY (`idProf`, `idEmpresa`),
  INDEX `idEmpresa_idx` (`idEmpresa` ASC) VISIBLE,
  CONSTRAINT `idProf`
    FOREIGN KEY (`idProf`)
    REFERENCES `mydb`.`Profesional` (`idProf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `idEmpresa`
    FOREIGN KEY (`idEmpresa`)
    REFERENCES `mydb`.`Empresa` (`idEmpresa`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
  
